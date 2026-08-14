# How It works 

## The basic pipline 

1. The FlySky reciver captures the stick inputs from teh controller
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

The network 
# Control Dynamics and Single - Layer PID implementation 

In this single layer configuration, the PID loop compares the target angle setpoints directly against the filter IMU anlges to produce output corrections for the motor mixer 

## Error Calculation and Derivative Kick Prevention 

When figuring out the derivative of the error directly from the derivative of error over dt, it creates a sharp motor spike ( derivatie kick ) which is when the receiver stick setpoint changes instantly. To fix this, the derivative term which tracks the change in measurent angle relative to the previous cycle instead of tracking the error. 

## Managing Ground Integral Windup 

With a single layer angle PID, it accumulates static angle errors suck as .15 deggres when stationary on the ground. This makes error makes the Ki integral term steadily increase and saturate the outRoll as the throttle increases. I took two solutiosn to solve thsi 

## Solution 1: Throttle Gated Integration 

This bascially didnt allow the I term to collect any memory of when the drone was on the ground. This was controlled by the tur

When the throttle is low where it is near 0, I made allowintegral false. This wipes out any accumulated error continuosly so I term stay zero.   

When the throttle is HIGH, allowIntegral becomes true which starts to add up error normally to correct for infligh forces like wind or weight imbalance. 





