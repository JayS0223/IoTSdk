# IOT SDK

[![Documentation](https://img.shields.io/badge/Read-Documentation-blue)](https://docs.videosdk.live/flutter/guide/video-and-audio-calling-api-sdk/concept-and-architecture)
[![Discord](https://img.shields.io/discord/876774498798551130?label=Join%20on%20Discord)](https://discord.gg/bGZtAbwvab)
[![Register](https://img.shields.io/badge/Contact-Know%20More-blue)](https://app.videosdk.live/signup)


At Video SDK, we’re building tools to help developers bring **real-time collaboration** to IoT and embedded devices. With the IoT SDK, you can integrate **live audio communication, meeting management, device-to-cloud connectivity, and session handling** directly into ESP32.

## Prerequisites

- Python >= 3.11
- A valid [Video SDK Account](https://app.videosdk.live/)

## Use IoT SDK Component

Follow these steps to use the IoT SDK component in your project:

### 1. Configure ESP-IDF enviorment 

- For setting up **ESP-IDF**, follow only **Step 1** from videosdk's [documentation](https://docs.videosdk.live/iot/guide/video-and-audio-calling-api-sdk/quickstart/quick-start#step-1-setup-for-esp-idf).
- Inside Step 1, you **do not need to run the project creation commands** — 
```
// Create an esp-idf project
cd ~/esp
idf.py create-project your-project-name
cd your-project-name
```
Once the tools and environment are set up, jump directly to **Step 2 in this README**.

### 2: Add IoT SDK component

Add the IoT SDK dependency to your ESP-IDF project. This includes all required libraries to use IoT SDK features in your project.  

```
idf.py add-dependency videosdk/iot-sdk:^0.0.1
```

```
dependencies:
    iot-sdk: 0.0.1
```

### 3. Generate a token from [VideoSDK's Dashboard](https://app.videosdk.live) and modify the token variable in `quick_start.c` file
```
const char *token = "GENRERATED_TOKEN"; // Your VideoSDK Authentication token
```

### 4. Build & Flash Project

Configure, build, and flash the firmware onto your ESP32 board. This compiles the code, applies the configurations, and uploads it to your device.
```
1. <!-- Run this command to set your board as the target-->
idf.py set-target esp32-s3

2. <!-- Run this command to do menuconfig -->

idf.py menuconfig  

         a. Inside the component config:
                |
                |———> mbedtls
                      | ——>Enable Support DTLS    <!-- It enables 3 way handshake  -->
                      | ——>Enable Support TLS      <!-- It enables 3 way handshake  -->
          And click S to save and again enter       

          b. Inside Example Connection Configuration:
                |
                |———> WIFI SSID         <!-- replace it with your WiFi name  -->
                |———> WIFI Password     <!-- replace it with your WiFi password -->
          And click S to save and again enter 

          c. Inside the Partition table :
                |
                |———> Partition table (custom partition table CSV)        
                      |———> Enable Custom partition table CSV

          d. Adjust the flash size inside Serial flasher config 
             (because some boards have limited flash memory)
                | ——> flash size: 2MB (esp32s3 XIAO sense)
                | ——> flash size: 4MB (esp32s3 qorvo2 v3.1)
          And click S to save and again enter

          e. Inside the Set Microcontroller : 
                | ——>**Audio hardware board (example : ESP32-S3-Korvo-2)**
                      | ——> Select your board name
                              |———> ESP32-S3-XIAO       
                              |———> ESP32- ESP32-S3-Korvo
          And click S to save and again enter

3. <!-- Run this command to build the project  -->
idf.py build

4. <!-- Run this command to flash the project to your microcontroller -->
idf.py flash monitor 
```

## Documentation

- For more details, check out the [VideoSDK Documentation](https://docs.videosdk.live/iot/guide/video-and-audio-calling-api-sdk/concept-and-architecture)






## Documentation

For more details, check out the [VideoSDK Documentation](https://docs.videosdk.live/iot/guide/video-and-audio-calling-api-sdk/concept-and-architecture)

