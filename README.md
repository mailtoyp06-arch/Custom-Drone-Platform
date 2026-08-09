# Custom-Drone-Platform
<p align="center"> <img src="media/drone_full_build.jpg" width="300"> </p> <!-- ✏️ EDIT: swap in your own photo filename above, or delete this block until you have one -->
Custom Autonomous Quadcopter Platform
<p align="center"> <img src="https://img.shields.io/badge/Platform-Arduino-red?style=flat-square"> <img src="https://img.shields.io/badge/Language-C%2B%2B-blue?style=flat-square"> <img src="https://img.shields.io/badge/PCB-Custom%20Design-orange?style=flat-square"> <img src="https://img.shields.io/badge/License-MIT-lightgrey?style=flat-square"> </p> <!-- ✏️ EDIT: update/add badges — e.g. swap "Arduino" for your actual flight controller/MCU, add a "Status-In Progress" badge -->

I built a custom-built quadcopter, specifically, the frame, custom PCB, and flight control firmware, with off-the-shelf components (motors, ESCs, sensors) integrated into the system. Built in two variants: a manually piloted RC version and an autonomous version.

This drone uses a ESP32 to controll the whole drone where it has 4 motors to controls its rolling, pitch and yaw and uses a lipo battery. This first version of the drone is was just for the RC version. The second version here is for both RC and autonmous where the second version from the mistakes of the first one and and made to be bigger to handle more compenents need be.  -->

⚠️ This repository is still being documented — more build notes and diagrams will be added soon.

# 🌍 Project Background

The reason I started this project was since I wanted to do somethign over summer isnstead of just take courses where I though doing a personal project on desighnig and building a drone from scratch would sound cool. I would learn so much new stuff and revist topics that I would actually use in this project. I also knew this would be a big challenge since I am not good at coding and does take time for me to undertand how the logic would work. But I knew by doing this, I would gain skill in both coding, electrical stuff and new mechcanical knowledge 

The result the drone will be able to do:

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
|ESC|provides PWM singals at right time for motors to spin|
|Motors|flys the drone by providing thrust|
|PLA / PLA+ frame|hold all compenetns together so it can all fly in one peice|
|battery|Power source|

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
   Before the drones takesoff, small anggles from roll, pitch and yaw caused the PID integral term to conninuosly acculmate. Thsi integral windup saturated motor outputs and cuased erractic flips upon arming. Gating the integrator accumilation until throttle passes hover threshold and addaing dyanmic anti windup clamping prevented the motor saturation and stablizedd groudn to air transitinos. 
3. **Modular PCB hardware**
    Directly sodler the sensitve compents like the ESP32 and the IMU to a custom PCB left them really vulnerable to physcial crash impacts and power shorts. Mounting compents onto female header soceksr decoupled teh mechancial stres wwhich created a sacrifical layer for crash impactact and enabled instatn compnet swaps without re-sodler the base board.  
5. **Yaw snapback from magnometer control**
   The targetign system tracked absolute north of the Earths mangetic lines which caused the lfight contrller to fight pilot stick inputs and snap back aggresseviely when sticks were realeased or local mangetic interfeces occurred. Changing the yaw axis from absolute heading control to gyro rate control loop allowed smooth stick commands while holding steady relative heading when hands off. 
7. **Bus contention, WDT resets and timing spikes**
The overlap across I2C,SPI and UART peripherals combined with blocking Serial.print() calls inside the core control loop caused the ESP32 watchdog Timer (WDT) panics and memory corrutppion. Restructuring perpheral pin assighments, removing blocking serial calls fomr the fast loop, and enforcing non blocking millis() timing schhedules resotred determinsitc 250Hz ececution.

# 🚀 Getting Started
<!-- ✏️ EDIT: fill this in once your code is actually in the repo — this is a placeholder structure based on a typical embedded/Arduino project -->
1. Clone the repo
bash
git clone <!-- ✏️ EDIT: your repo URL -->
cd <!-- ✏️ EDIT: repo folder name -->
2. Hardware setup
<!-- ✏️ EDIT: list what someone needs to wire up / assemble before flashing firmware -->
3. Flash the firmware
<!-- ✏️ EDIT: e.g. Arduino IDE steps, board selection, upload instructions -->
4. Power on and test
<!-- ✏️ EDIT: what should happen when it powers on correctly? -->
📌 Repo Status
<!-- ✏️ EDIT: check these off honestly as you go, add/remove lines as needed -->

✅ <!-- ✏️ EDIT: e.g. "Initial liftoff achieved" -->

🔧 <!-- ✏️ EDIT: e.g. "PID tuning for stable hover — in progress" -->

⬜ <!-- ✏️ EDIT: e.g. "Autonomous waypoint navigation — not started" -->

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
