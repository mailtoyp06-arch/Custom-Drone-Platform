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
| Main | Reads WebSocket events, drives the filter state machine |
| ESC | keeps readign PWM signals from the ESP32 |
| Reciver | keeps waitign for singals from flysky controller so it can give to ESP32 |
| Bluetooth watchdog | Independently monitors and recovers the Bluetooth connection |
| IMU sensor | non stop data coming into ESP32 for kalman filter and PID to get processed by ESP32 |

