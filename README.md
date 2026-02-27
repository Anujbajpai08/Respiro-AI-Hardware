# Respiro AI – Embedded Hardware Module

## Overview
This project focuses on designing and implementing a low-cost embedded respiratory monitoring system. The goal is to develop a hardware module capable of sensing breathing patterns and enabling future integration with AI-based analysis systems.

## Problem Statement
While AI models can analyze respiratory data effectively, many systems lack affordable and portable hardware modules for real-time breath acquisition. This project aims to bridge that gap.

## Objective
- Design a breath sensing hardware architecture
- Select appropriate sensors and microcontroller
- Implement signal acquisition and processing
- Enable future AI integration

## System Architecture
![System Block Diagram](system_block_diagram.png)
## Block-Level Explanation

### 1. Mouthpiece / Mask
Captures airflow during inhalation and exhalation and channels it through tubing to the differential pressure sensor.

### 2. Differential Pressure Sensor (MPXV7002DP)
Measures the pressure difference created by airflow. The output is a small analog voltage proportional to breath intensity.

### 3. Instrumentation Amplifier (INA333 / AD623)
Amplifies the low-level differential signal from the sensor while rejecting common-mode noise.

### 4. ADS1115 (16-bit ADC)
Converts the amplified analog signal into high-resolution digital data for accurate breath waveform capture.

### 5. ESP32
Processes digital data, performs filtering and respiratory rate calculation, and transmits data via WiFi or serial interface.

## Hardware Components
## Procurement Status

| Component | Selected | Purchased | Tested |
|------------|----------|------------|--------|
| ESP32 DevKit | Yes | yes | yes |
| MPXV7002DP | Yes | yes | yes |
| INA333 / AD623 | Yes | yes | yes |
| ADS1115 | Yes | yes | yes |

## My Contribution
- Participated in AI system conceptual discussions
- Leading hardware architecture design
- Sensor research and selection
- Embedded system implementation

## Current Status
Hardware planning and architecture design phase.

## Future Scope
- Edge AI deployment
- IoT-based respiratory monitoring
- Low-power system optimization
