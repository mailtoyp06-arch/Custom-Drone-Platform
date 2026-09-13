# Custom-Drone-Platform
<p align="center"> <img src="media/drone_full_build.jpg" width="300"> </p> <!-- ✏️ EDIT: swap in your own photo filename above, or delete this block until you have one -->
<p align="center"> <img src="https://img.shields.io/badge/Platform-Arduino-red?style=flat-square"> <img src="https://img.shields.io/badge/Language-C%2B%2B-blue?style=flat-square"> <img src="https://img.shields.io/badge/PCB-Custom%20Design-orange?style=flat-square"> <img src="https://img.shields.io/badge/License-MIT-lightgrey?style=flat-square"> </p> <!-- ✏️ EDIT: update/add badges — e.g. swap "Arduino" for your actual flight controller/MCU, add a "Status-In Progress" badge -->

I built a custom-built quadcopter, specifically, the frame, custom PCB, and flight control firmware, with off-the-shelf components (motors, ESCs, sensors) integrated into the system. Built in two variants: a manually piloted RC version and an autonomous version.

This drone uses a ESP32 to controll the whole drone where it has 4 motors to controls its rolling, pitch and yaw and uses a lipo battery. This first version of the drone is was just for the RC version. The second version here is for both RC and autonmous where the second version from the mistakes of the first one and and made to be bigger to handle more compenents need be.  -->

⚠️ This repository is still being documented — more build notes and diagrams will be added soon.
# Drone Photos 

<p align="center">
  <img src="https://github.com/user-attachments/assets/f5143fc7-e2e9-4247-9d5d-f6f634abff91" width="45%" />
  <img src="https://github.com/user-attachments/assets/7af534e3-ead7-43d5-9ec7-85f47e75edce" width="45%" />
</p>
<p align="center">
  <img src="https://github.com/user-attachments/assets/c8547664-ecc2-4fac-83ec-34b9aaceaf20" width="45%" />
  <img src="https://github.com/user-attachments/assets/184fa118-18dd-40aa-a645-10e70b1b001a" width="45%" />
</p>

# 🌍 Project Background

The reason I started this project was that I wanted to build something over the summer instead of just taking courses. I thought doing a personal project on designing and building a drone from scratch would be a great way to learn. It allowed me to pick up new skills and revisit core concepts directly applicable to the build. I knew it would be a major challenge since programming takes time for me to master, but tackling it helped me build strong foundations in embedded coding, electronics, and mechanical design.

The results the drone will be able to achive:

 - Able to activly change the drone settigns as freely need be
 - evntually be able to go from Point A to B autonmously
 - Runs on a self-designed PCB rather than an off-the-shelf flight controller meaning easier control of drone and change space configuration in drone
 - This drone costed about $150 for the RC version and $180 for the autonomous version 

# 🛠 System Overview
## Hardware
Component	Purpose
| Component | Purpose |
|-----------|---------|
|ESP32|Main controller, runs flight firmware|
|Custom PCB|Power distribution and signal routing|
|ESC (GForces 30A Brushless)|provides PWM singals at right time for motors to spin|
|Motors ( A2212 Brushless motors )|flys the drone by providing thrust|
|PLA / PLA+ frame|hold all compenetns together so it can all fly in one peice|
|battery (9 ManiaX 3S 2200 mAh) |Power source|
|IMU Sensor (Adafruit LSM9DS1 Board)|gets gyro, accelerometer and magnometer data|
|Thin Guage Wires ( 28AWG Silicone Wires) |wires for sending data from pin to pin under PCB|
|PDB (PDB XT60 power distribution Board BEC) |Board to handle sending power from main battery to all 4 brusheless motors |
|Radio Reciver (FS - iA6 Reciver Set) | recives radio signlas from RC controller |
|Radio transmitter (FLYSKY FS-i6x) | transmitts radio signlas to Radio Reciver |





Hardware diagrams and wiring can go in a hardware/ folder once you have them.

# 🧩 How It Works
<!-- ✏️ EDIT: once you have a wiring or system diagram, embed it here like this: <p align="center"> <img src="hardware/system_architecture.png" width="550"> </p> -->

## The flight pipeline

<p align="center">
  <img src="https://github.com/user-attachments/assets/2c0cc548-c740-48b1-85a0-4cb8a56d6fbe" width="600" alt="System Architecture">
</p>

1. **RC controller** - Data comes from the flysky controller which is captured by the reciver.
2. **IMU sensor:** - IMU reads orientation data has 9 axises of rotation which is sent to ESP32.
3. **Calculation by ESP32** - The ESP32 then takes the RC controller singnals, IMU data and then puts the IMU data through a complemntary filter which is then used in a PID loop with flysky controller.
4. **ESC signals** - ESCs adjust the motor speed and stabilty by the sent PWM signals from ESP32. 
5. **Motors** - PWM signals gotten from ESC is sent to motors which then spins based on PWM signals from ESC.
# Two Variants of Drone 
## RC Version
In RC mode, drone is controlled by using RC controller which sends signal to control drone. 
## Autonomous Version
In autonomous mode, the drone will be able to go from point A to point B using a ground station which sends data to ESP32 for drone to go to. RC controller still needed when need to overide autonomous mode.
# 🧠 Notable Engineering Problems
1. **PID integral windup and motor saturation**
   Before takeoff, small error angles in roll, pitch, and yaw caused the PID integral term to continuously accumulate. This integral windup saturated motor outputs and caused erratic flips upon arming. Gating integrator accumulation until throttle passes the hover threshold and adding dynamic anti-windup clamping prevented motor saturation and stabilized ground-to-air transitions.
3. **Modular PCB hardware**
  Directly soldering sensitive components like the ESP32 and IMU to a custom PCB left them vulnerable to physical crash impacts and power shorts. Mounting components onto female header sockets decoupled mechanical stress, creating a sacrificial layer for crash impacts and enabling instant component swaps without resoldering the base board. 
5. **Yaw snapback from magnometer control**
   The targeting system tracked absolute north along Earth's magnetic field lines, causing the flight controller to fight pilot stick inputs and snap back aggressively when sticks were released or local magnetic interference occurred. Changing the yaw axis from absolute heading control to a gyro rate control loop allowed smooth stick commands while holding a steady relative heading when hands-off.
7. **Bus contention, WDT resets and timing spikes**
The overlap across I2C, SPI, and UART peripherals combined with blocking Serial.print() calls inside the core control loop caused ESP32 Watchdog Timer (WDT) panics and memory corruption. Restructuring peripheral pin assignments, removing blocking serial calls from the fast loop, and enforcing non-blocking millis() timing schedules restored deterministic 250Hz execution.

# 🚀 Getting Started

## 1. Hardware Assembly and Wiring Setup
* **IMU Sensor:** Connect the IMU using I2C. Connect the SCL pin to GPIO 22 and the SDA pin to GPIO 21. Ensure the rubber grommets are installed on the base plate for mechanical vibration isolation.
* **FlySky Receiver (FS-iA6B):** Connect the i-BUS RX wire to GPIO 16.
* **ESCs (4 x 30A):** Connect the PWM signal wires to GPIO 13 (front right), GPIO 12 (rear right), GPIO 14 (rear left), and GPIO 27 (front left).
* **Power Distribution:** Verify that the 3S LiPo voltage steps down through a 5V converter on the PDB, which then supplies clean power directly to the ESP32 5V pin, bypassing motor EMF spikes.

## 2. Flash Firmware via Arduino Software 
1. Open the project folder where VS code is and all librarys are installed
2. Connect you ESP32 board via USB-C/Micro-USB
3. Open Arduino and make sure you have right ESP32 board connected and upload_speed at 921600
4. Hit run or send to flash code to ESP32

## 3. Bench Test and Verification Safety 
1. REMOVE ALL PROPELLERS before powering on with the battery connected.
2. Open the Serial Monitor and verify it is set to a 115200 baud rate.
3. Power on the FlySky controller and the FlySky receiver.
   - Verify the IMU reports roll, pitch, and yaw angles near 0 degrees when the drone is placed on a flat surface.
   - Check that the receiver is sending and receiving signals within the 1000 to 2000 microsecond range. Perform a visual check; if signal response is laggy, adjust the receiver update rate.
     
📂 Repository Structure
<!-- ✏️ EDIT: update this to match your actual folder layout once files are uploaded -->
<!-- ✏️ EDIT: repo-name -->/
│
├── firmware/
│   └── <!-- ✏️ EDIT: main firmware file -->
│
├── cad/
│   └── <!-- ✏️ EDIT: frame/mount design files -->
│
├── hardware/
│   └── <!-- ✏️ EDIT: wiring diagrams, PCB files -->
│
├── media/
│   └── <!-- ✏️ EDIT: build photos -->
│
├── .gitignore
├── LICENSE
└── README.md
