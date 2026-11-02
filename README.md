![Robotics](https://img.shields.io/badge/Robotics-orange)
![Control Engineering](https://img.shields.io/badge/Control_Engineering-gold)
![IT](https://img.shields.io/badge/IT-purple)
![Electronics](https://img.shields.io/badge/Electronics-darkred)
![Mechatronics](https://img.shields.io/badge/Mechatronics-darkgreen)


![Hardware](https://img.shields.io/badge/Hardware-blue)
![Software](https://img.shields.io/badge/Software-lightblue)


<p align="center">
<img src="./Readme_Images/Q_home.jpg" alt="Quadcopter" width="550"> <br>
<em>Designed and assembled by me.</em>
</p>

# Aerial Robotics Research Platform



My Bachelor's project's task is to develop a platform for experimentation in flight control, state estimation, feedback control, trajectory planning, and GPS-denied localization.

Rather than relying on an off-the-shelf flight controller, the system is developed from the ground up: from the mechanical and electronics hardware to the embedded software, estimation algorithms, and UWB positioning infrastructure.

The flight-controller is implemented without using any specific libraries for sensors, control, or state estimation; instead, a low-level framework is developed using HAL for STM.

Development time: from 01.2026 to 02.2027 (expected graduation). After that I will continue with the project anyway.

The project is also referred to as "Day One".

<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="Readme_Images\DayOne_Logo_White_on_Github.png">
    <source media="(prefers-color-scheme: light)" srcset="Readme_Images\DayOne_Logo_Black_on_White.png">
    <img alt="Logo" src="Readme_Images\DayOne_Logo_White_on_Github.png" width="450">
  </picture>
</p>

**Note: This repository is just a portfolio, but I can share all design and source files with recruiters upon request.**

## Table of contents
* [Presentation](#presentation)
* [Current progress](#current-progress)
* [General Information](#general-information)
* [UWB Positioning System](#uwb-positioning-system)
* [Technologies Used](#technologies-used)

## Presentation

Below you can see pictures from the development process.

**Note: I have designed and assembled components listed below by myself:**
- main PCB (soldered manually)
- rotor guards and landing legs
- main carbon chassis
- transparent cover for the PCB
- supports and the uppermost cover for the PCB
- a battery case that allows for quick batteries switch
- ESC cover at the bottom

<p align="center">
<img src="./Readme_Images/Q_front_no_prop.jpg" alt="Quadcopter" width="550"> <br>
<img src="./Readme_Images/Q_red.jpg" alt="Quadcopter" width="550">
<img src="./Readme_Images/Q_top.jpg" alt="Quadcopter" width="550"> <br>
<img src="./Readme_Images/Q_front_prop.jpg" alt="Quadcopter" width="550"> <br>
<img src="./Readme_Images/Q_side.jpg" alt="Quadcopter" width="550"> <br>
<em>Quadcopter in real life.</em>
 </p>

<p align="center">
<img src="./Readme_Images/Soldered_PCB.jpg" alt="Main PCB" width="550"> <br>
<img src="./Readme_Images/PCB_2.jpg" alt="Main PCB" width="550"> <br>
<em>Main PCB.</em>
 </p>

<p align="center">
<img src="./Readme_Images/Quadcopter_Assembly.png" alt="Quadcopter Render" width="550"> <br>
<img src="./Readme_Images/Quadcopter_Front_Render.png" alt="Quadcopter Render" width="550"> <br>
<img src="./Readme_Images/Main_PCB_3D.png" alt="Main PCB" width="550"> <br>
<em>3D models.</em>
 </p>


<p align="center">
<img src="./Readme_Images/Parts/Battery_Case.png" alt="3D model" width="225">
<img src="./Readme_Images/Parts/Chassis.png" alt="3D model" width="225"> <br>
<img src="./Readme_Images/Parts/Transparent_Cover.png" alt="3D model" width="225">
<img src="./Readme_Images/Parts/Rotor_Guards.png" alt="3D model" width="225"> <br>
<img src="./Readme_Images/Parts/ground_plus_topcover.png" alt="3D model" width="225">
<img src="./Readme_Images/Parts/Bottom_First_Cover.png" alt="3D model" width="225"> <br>
<em>3D models of individual parts.</em>
 </p>

## Current progress
<p align="center">
<em>November 2026:</em>
 </p>

State estimation is being implemented. I have derived/noted all necessary matrix equations for linear and angular motion. Now I will implement Kalman Filter in a low-level framework.

---

<p align="center">
<em>October 2026:</em>
</p>

Communication with the IMU and magnetometer is implemented. The STM performs necessary initializations, transfers, and data conversions. This is achieved without using any specific libraries for the sensors; instead, I read the datasheets and implement a low-level interface between the MCU and other chips. For the moment, measurements from the IMU are read at a 1kHz update rate, and at 100Hz from the magnetometer.

Ground station is complete. It consists of a MATLAB program connected to an ESP32 via USB. It allows for:
- fine-tuning position estimation of the lighthouses,
- changing parameters of the process,
- general communication with the drone and lighthouses.

---

<p align="center">
<em>September 2026:</em>
 </p>


The quadcopter has been assembled and it passed all the necessary hardware tests. That means the motors work, all chips are soldered correctly, and nothing is overheating. It lifts at around 35% motor power, and the battery lasts around 5 minutes in that setting.

---

<p align="center">
<em>July 2026:</em>
 </p>

The main PCB has been soldered manually and tested. The electronics schematic is avaiable in this file:
[PCB_Schematic/Quadcopter_Main_PCB_Schematic.pdf](./PCB_Schematic/Quadcopter_Main_PCB_Schematic.pdf)

## General information

### Control Engineering
- Implementing a:
    - cascade 4-loop PID controller,
    - Kalman filter state estimator,
    - If time allows: polynomial decoupled trajectory planning based on given setpoints.
- Utilizing quaternions for attitude representation enabling more stable orientation control.
- If time allows: synthesizing a mathematical model of the drone to enable tuning the algorithms in simulation.
- Enabling manual override of the speed or attitude commands.


### Electronics
- An STM32F4 is used as the main MCU.
- An ESP32 onboard provides communication with a ground station and a custom positioning system (described later).
- IMU and a magnetometer support the positioning system in state estimation.
- Power source is a 680mAh, 3S, LiHV battery.
- Propellers are mounted on BLDC motors for high efficiency and power.
- The onboard power converter steps the voltage down to 3.3V.
- Safety measures are implemented to protect the device from overcurrent, overvoltage, reverse polarity, and ESD events.
- An off-the-shelf ESC drives the motors, commanded by the MCU's DShot or PWM signals.


### Mechanics
- Designing custom:
    - carbon base plate for the robot,
    - housing for the PCBs,
    - shielding frame around the propellers,
    - battery slot.
- The rotor guards and landing legs have been prototyped a few times to assure they could protect rotors during crash.
- The battery slot was designed with care to assure quick and comfortable battery replacement. It has a dedicated recess for a finger to grab the battery. Also, the battery does not jam or get stuck by its wires when removing.
- Total weight is 242 grams, which fits within the constraints set by the propellers' thrust: the drone lifts at around 35% motor power.

## UWB Positioning System
Part of the project is a custom positioning system that doesn't rely on a GPS signal. This is achieved by placing at least 4 Ultra-Wideband (UWB) modules near the area of the drone's operation. They measure their distance to the robot and estimate its relative position. This system is almost fully developed, and can be seen in this repository: [https://github.com/A-Rozmarynowicz/UWB_Positioning_System](https://github.com/A-Rozmarynowicz/UWB_Positioning_System).

<p align="center">
<img src="./Readme_Images/UWB_rl.jpg" alt="./Graphics/Readme_Images/UWB_PCB_3D_Image.png" width="550">
<img src="./Readme_Images/UWB_PCB_3D_Image.png" alt="./Readme_Images/UWB_PCB_3D_Image.png" width="550"> <br>
<em>UWB anchor.</em>
 </p>



## Technologies Used
- Ultra-Wideband radio technology
- Communication protocols: SPI, I2C, UART, ESP-NOW, PWM, DShot

- Control engineering:
    - cascade PID
    - Kalman filter
    - state machines
    - polynomial decoupled trajectory calculation

- Programming languages:
    - C
    - C++
    - MATLAB

- Software used:
    - STM32 Cube IDE
    - Altium Designer
    - Autodesk Fusion
    - MATLAB
    - PlatformIO
