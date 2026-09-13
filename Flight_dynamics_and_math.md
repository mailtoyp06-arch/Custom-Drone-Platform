# Angle Calculation from IMU data 
## Correct Data calculation from Raw Data  
aw data directly from the IMU can be noisy and inaccurate. To ensure precise measurements, I first calibrated the IMU to calculate its zero-offset, as factory sensors inherently carry small measurement errors. Using an IMU calibration tool, I calculated the offsets and scaling factors across the X, Y, and Z axes for the gyroscope, accelerometer, and magnetometer: 
  - For the gyro, I averaged the raw data across all three axes while stationary to determine the baseline zero-offset.
  - For the accelerometer, While rotating the sensor across all three axes, I captured the average raw data baseline and subtracted $1\text{ g}$ (Earth's gravity) to determine the Z-axis offset. 
  - For the magnometer, I recorded the maximum and minimum raw values across a full 360-degree rotation on each axis to find the center offset (averaging the min and max divided by 2). I then computed the average range across all three axes divided by each individual axis range to determine the scaling factor for the X, Y, and Z axes. 

## Calculating Angles from Correct data 
Once all the data from teh IMU is right based on those offsets and scaling factors, I calculated the angles for roll, pitch and yaw. 
  - For roll, I used `(atan2(ax, az) * 180.0 / PI - ANGLE_OFFSET_ROLL)'. 
    - Atan2(y,x): calucalted ratio of two acceleration components, ax and az 
    - * 180 / PI: puts the result in degrees from radians 
    - - ANGLE_OFSET_ROLL: with the IMU sensor itself calibrated, it can be .5 or even 1 degree off relative to the frame so uses the angle offset roll to always put it on 0 degrees when drone on ground 
  - For Pitch, I used 'atan2(-ay, sqrt(ay * ay + az * az)) * 180.0 / PI + ANGLE_OFFSET_PITCH`
    - atan2 and the varibels I used is ay and square root of (ay * ay + az * az)
    - + ANGLE_OFFSET_PITCH is the same reason as the roll 
## Using the Complemntary Filter 
Once the both angles for roll and pitch are gotten, we us a complementary filter / fusion filter to correct for anlge drift 
  - For rolling angle it is `angleRoll = COMP_ALPHA * (angleRoll + gyroRoll * dt) + (1.0 - COMP_ALPHA) * -accRoll'
    - The angleRoll + gyroROlll * dt is trust the gyro 98% of the time sicne gyro is extrmely responsive for measuring fast angule rate changes withou interfeces from translational forces or motor virbation. 
    - The (1.0 - COMP_alpha is only trusted 2% of the time since it suffers from vibratison, linear acceleratiosn and sudden body motion but for the long term, it doensnt acumilate drift which is why it is trusted only 2% of the time to fix gyro drfit. 

# PID calculation for balanced flight 
The PID is where everything comes together. More specifcally, the data from the IMU and the radio signals from the RC controller come here to see how much output needed for motors based on those vairbles. 

The PID works on 9 varibles which is PIDroll, cmdRoll, angleRoll, ROLL_kp, ROLL_ki,ROLL_kd,PID_out_limit, dt, allowI). This is just for the 



# Intial Varibles for PID, Complementary Filter and IMU 
## Scaling of Pilot controls 
| Varible | Purpose |
|-----------|---------|
|Max tilt angle degrees = 30| full roll/pitch stick commands this lean angle  |
|Max yaw rate DPS = 150 | full yaw stick commands this rotation rate (deg/s) |
|Arming throttle Max = 1090| Throttle must be below this to arm (safety) |
|Motor start throttle = 1100 | above this input, the stabiliser mixes corrections kicks in|

## PID varibles 
| PID Varible | Purpose |
|-----------|---------|
|cmdRoll | maximum range or roll angle in degrees   |
|angleRoll| desired roll angle of drone when gotten from RC controller  |
|ROLL_KP| the gain factor for immediate error correction|
|ROLL_KI| The gain factor for acccumilating persisten past errors |
|ROLL_KD| The gain factor that reacts to how fast the error is changing |
|dt| the exact time elapsed sicne last PID execution in seconds|
|allowI| A bollean true/ false that enables or disables accumilation of integral term I |

With these varibles defined I take each of these varibels for either roll, pitch or yaw. they all work on the same function 
1. figure out the P using kp * error. 
2. Use our first dual layer anti windup mechanism which is for the I term building up. This happens since when on the ground the error can addup even if you are slightly of center which is why I added this. 
The code which is `  if (allowIntegral) {
    s.integral += ki * error * dt;
    s.integral = constrain(s.integral, -I_LIMIT, I_LIMIT); // added here 
  } else {
    s.integral = 0.0f;
  } ' takes ki * error * dt. That integral term then gets constrainted within the limits or it becomes 0. 
3. Get D derivative from angle of yaw,pitch or roll - previous angle of either of those 3 over dt. Then I used a EMA filter which used a low pass filter to the raw derivative value. Finally get real D term by using kd * that filter value of real d term.  
4. For the actuall output, we then add the P, I and D term to get our actual output for the motors. 


