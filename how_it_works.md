# How It works 

## The basic pipline 

1. The FlySky reciver captures the stick inputs from teh controller
2. stick inputs from controller goes to ESP32 as well as data from IMU sensor
3. The data from the IMU sensor is capture and put through the complemntary filter
4. The stick inputs and the filter data from IMU is put through a PID for motor output
5. Once PID is finsihed, output PWM siginals sent to each ESC
6. motor captures that ESC signals and outputs whatever it has gotten

## Numerous times threads running 

