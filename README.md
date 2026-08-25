                                                  Haptics & Motion Controller Glove
                                                             By Koray

![image alt](https://github.com/koray9012/The-immersion-glove-/blob/main/15502.jpg?raw=true)

A custom-built, motion-controlled ESP32 air mouse glove featuring dynamic haptic feedback, motion-freeze capabilities, and live python telemetry integration designed for PC gaming and heavy weapon control in *Helldivers 2*.

## Key Features

  6-DOF Motion Tracking:

  • Uses an MPU6050 6-axis gyro/accelerometer to read smooth pitch and yaw rates for real-time cursor positioning with custom low-pass filter smoothing and deadzone filtering.

  Dynamic Transistor-Driven Haptic Engine:

  • Driven via NPN transistor on GPIO 23, delivering instant recoil impulses, secondary weapon fire profiles, and continuous variable PWM charge effects.

  Helldivers 2 Support & HUD Scanner:

  • Features a Python host application equipped with real-time OpenCV screen-grabbing via `mss` to automatically detect equipped support weapons (Quasar Cannon, Autocannon, Recoilless Rifle) and dynamically map active haptic feedback profiles.

  On-Glove Hardware Controls:

  • Dedicated ergonomic finger switches for Left Click (LMB/Trigger), Right Click (RMB/ADS), Motion Freeze Toggle (Pin 14), and Scroll / Mode Selection (Pin 27).

  Low-Latency Serial Interface:

  • Streams raw 125Hz 6-DOF motion arrays directly over USB-UART to a lightweight Python driver with Win32 `ctypes` direct mouse input mapping.

## How to use:

To use it first you need to connect the ESP32 to your PC via micro-USB and launch the Python driver (`python glove-mouse.py`). Once connected, moving your hand rotates the crosshair using pitch and yaw. The finger switches act as Left Click (LMB) and Right Click (RMB), while the auxiliary switches let you freeze motion or toggle modes. For *Helldivers 2*, press `3` on your keyboard while in-game to activate OpenCV screen detection—it will scan your HUD for support weapons like the Quasar Cannon or Autocannon and automatically assign customized haptic recoil feedback patterns to your glove.

Here is so clean instructions on how to do it step by step:

## Operating Instructions
1. Power On & Connect
  1.Connect the ESP32 on the glove to your PC using a micro-USB data cable.

  2.Check that the MPU6050 power LED illuminates to verify 3.3V power.

2. Launching Driver
  1.Open terminal on your PC, navigate to the folder, and run `python glove-mouse.py`.

  2.The script automatically binds to the ESP32 COM port and starts mouse emulation.

3. In-Game Control & Haptics
  1.Tilt your hand up/down (pitch) and left/right (yaw) to aim the cursor.

  2.Use finger buttons for LMB (Trigger) and RMB (ADS).

  3.Press the Motion Freeze button (Pin 14) to temporarily lock aiming while typing or taking a break.

  4.Press key `3` in the terminal to activate HUD scanning for *Helldivers 2* heavy weapon profiles.

## Why I made it:

After working with custom embedded microcontrollers and basic telemetry, standard mouse and keyboard setups felt unimmersive for fast-paced tactical shooters like *Helldivers 2*. I wanted to build a hands-on, wearable controller that bridges physical hand gestures directly into crosshair movement while adding physical haptic feedback that standard gaming peripherals lack.

I designed this project to combine low-latency serial communication, custom sensor filtering, and hardware haptics into a single wearable chassis. Switching from raw gyro data to filtered relative cursor movement was a huge challenge, as was managing Python thread execution so continuous haptic PWM signals didn't introduce latency into crosshair movements. Building this glove provided a deep dive into I2C sensor registers, Win32 input API handling, custom haptic driver circuit design, and computer-vision HUD recognition.

### Wiring & Connections:

Below is the visual schematic diagram for the Haptics & Motion Controller Glove.

![image](https://github.com/koray9012/Haptics-Motion-Glove/blob/main/schematic.png?raw=true)

### Pinout Breakdown:

| ESP32 Pin | Component | Connected Pin / Note |
| :--- | :--- | :--- |
| **GPIO 23** | NPN Transistor Base | Vibration Motor PWM Control |
| **GPIO 21** | MPU6050 | Shared I2C SDA |
| **GPIO 22** | MPU6050 | Shared I2C SCL |
| **GPIO 13** | Left Mouse Button (LMB) | Trigger Switch (Pin to GND) |
| **GPIO 12** | Right Mouse Button (RMB) | ADS Switch (Pin to GND) |
| **GPIO 14** | Motion Freeze Toggle | Pushbutton (Pin to GND) |
| **GPIO 27** | Scroll / Mode Select | Pushbutton (Pin to GND) |
| **3V3** | MPU6050 | VCC (3.3V Power) |
| **5V / VBUS** | Vibration Motor | Motor Positive (+) Rail |
| **GND** | Shared System GND | Shared GND Rail across all switches & sensors |

## Code:

The code can be found in repo: Haptics & Motion Glove Code

## Bill of materials:

| Item | Quantity | Price (USD) | Link |
| :--- | :--- | :--- | :--- |
| Esp32 38 pins | 1 | 8.89 USD | https://www.ardboard.com/index.php?route=product/product&product_id=413 |
| MPU6050 6-Axis Module | 1 | 5.90 USD | https://elimex.bg/product/74823-kit-k2083-akselerometar-i-zhiroskop-za-uno-mpu6500 |
| Micro Vibration Motor | 2 | 3.52 USD x2 = 7.04 USD | https://elimex.bg/product/88708-motor-1.3-7vdc-ng04-6-vibromotor |
| 2N2222 NPN Transistor & Resistors | 1 | 0.15 USD | https://elimex.bg/product/87794-2n2222a-to-92 |
| Buttons | 4 | 0.30 USD x4 = 1.20 USD | https://elimex.bg/product/84643-microbuton-12-12-h-7-3 |
| Wearable Glove Base & Straps | 1 | 5.00 USD | DIY / Fabric Base |
| Jumper Cables | ~30 | 2.86 USD | https://elimex.bg/product/75823-komplekt-provodnitsi-40-broya-s-konektori-mazhki-zhenski-30sm |

## Very important: The custom wire harnesses were cut to size, heat-shrink sleeved, and hand-soldered directly to finger switch contacts.

## Video for glove demo (https://youtu.be/3u9llfJvqeY)

## Credits:

This project uses:

Kicad

OpenCV & MSS Python Libraries

Hack Club Macondo

Btw thank you for the Power Supply Hack Club :)
