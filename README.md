# ESP32 GoPro control for an FPV drone

Setup notes for adding GoPro recording control and live camera status to my custom FPV drone, using an ESP32-C3 SuperMini running the RECon32 firmware.

## Credit

The firmware is [RECon32](https://recon32.es/), free community software by its own developer. I did not write it, and its firmware files are not in this repo. This repo documents how I integrated it with my drone.

## What it does

- The ESP32 connects to a UART on the flight controller and talks to Betaflight over MSP
- A switch on my radio transmitter starts and stops GoPro recording
- Camera status shows up in the OSD in my goggles

## Demo

Short clip of the transmitter switch triggering the camera:



https://github.com/user-attachments/assets/46489cfd-ae75-407c-b35e-6205b9752798


## Result

Camera status in the goggles OSD: CAM READY and the camera mode.

![Goggles view showing CAM READY and the camera mode](images/goggles-cam-ready.jpg)

The same status line with the camera battery level.

![Goggles view showing CAM READY and the camera battery](images/goggles-cam-ready-battery.jpg)

## What I did

- Flashed the ESP32-C3 SuperMini with RECon32 using its web installer
- Wired the ESP32 to a free UART on the flight controller
- Set up a radio channel and the Betaflight OSD so a transmitter switch controls recording and status appears in the goggles
- Paired the ESP32 with the GoPro

## Wiring

I followed the RECon32 wiring guide for the ESP32-C3 SuperMini:

| Flight controller | ESP32-C3 SuperMini |
|---|---|
| 5V | 5V |
| GND | GND |
| UART TX | GPIO6 (RX) |
| UART RX | GPIO7 (TX) |

TX and RX are crossed, and the 5V goes only to the 5V pin, never to a GPIO. In Betaflight Configurator, MSP is enabled on the UART the ESP32 is connected to, at 115200 baud, as the guide says.
