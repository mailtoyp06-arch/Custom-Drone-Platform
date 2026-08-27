# How It works 

## The basic pipline 

1. The FlySky reciver captures the stick inputs from the controller
2. stick inputs from controller goes to ESP32 as well as data from IMU sensor
3. The data from the IMU sensor is capture and put through the complemntary filter
4. The stick inputs and the filter data from IMU is put through a PID for motor output
5. Once PID is finsihed, output PWM siginals sent to each ESC
6. motor captures that ESC signals and outputs whatever it has gotten

## Numerous times threads running 

| Thread | Job |
|--------|-----|
| Core 0: Comm and Telemtry | Handles non blocking Websocket / reciver telemtry logging and reads incoming FlySky receiver stick pulses |
| Core 1: Fast PID Loop | Runs on 1kHz update rate where change in time is 1 ms. Executes sensor reading, state filtering, PID calculaitons and ESC PWM writes |
| Watchdog and Fail-Safe | Monitors reciver pulse frames. Triggers emergency motor cut if no signal frame arrives within 200ms |

The network and telemtry tasks ran on core 0. 

# Control Dynamics and Single - Layer PID implementation 

In this single layer configuration, the PID loop compares the target angle setpoints directly against the filter IMU anlges to produce output corrections for the motor mixer 

## Error Calculation and Derivative Kick Prevention 

When figuring out the derivative of the error directly from the derivative of error over dt, it creates a sharp motor spike ( derivatie kick ) which is when the receiver stick setpoint changes instantly. To fix this, the derivative term which tracks the change in measurent angle relative to the previous cycle instead of tracking the error. 

## Managing Ground Integral Windup 

With a single layer angle PID, it accumulates static angle errors suck as .15 deggres when stationary on the ground. This makes error makes the Ki integral term steadily increase and saturate the outRoll as the throttle increases. I took two solutiosn to solve thsi 

## Solution 1: Throttle Gated Integration 

This bascially didnt allow the I term to collect any memory of when the drone was on the ground. This was controlled by a hard setpoint which would only be bypassed when hte throttle would exceed that threshold. 

When the throttle is low where it is near 0, I made allowintegral false. This wipes out any accumulated error continuosly so I term stay zero.   

When the throttle is HIGH, allowIntegral becomes true which starts to add up error normally to correct for infligh forces like wind or weight imbalance. 

## Solution 2: Direction Integral Clamping: 

When the error of the integrals started to overflow, I intially subtracted the s.integral fomr the (out - outlimit). The problem was that the s.integral is completely different unit which uses ms and out and outlimit uses a duty cycle which is differnt. The solution was instead have the s.integral just constrained instead of just removing the error every frame. 

# Sensor Filtering and Vibration Rejection 

## Software Low Pass filtering 

Flying the drone, it makes high frequency motor virbaitosn which corrupts the raw MPU6050 acceleometer measurments. This high freqency noise propagates into the derivative term whcih causes the motor to overheat and makes the frame shake erraticly 

To solve this, I used a 1st order Software Low Pass Filter (LPF) which was applied to the derivative term of roll, pitch and yaw. I used a alpha vale of.15 which means that the code only turst 15% of the brand new incoming reading and relies 85% on pas mossted history. This smooths out the sharp spikes. 

Along with complemntary Filter, it also belnded in the gyro and accelerometer data. This was due to the gyroscope being extremlly fast and accurate for the short term but driting over time of postion. Accelerometer is good at long term since uses gravity but bad for short term sicne the vibrations corrups the readings.   

So really the formula I used .98 * ( angle + Gyro rate * dt) + ( .02 * accelerometer angle) 

98% of it is on the gyro since during the intial 4 to 6 seconds, 98% of the drones angle relies stricly on the gyroscope while the 2% is on the accelerometer weight. The 2% bascially coorects any long term drift the gyroscopes introduce without lettign vibration noise corrupt the data and loop. 




