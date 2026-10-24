<img width="337" height="243" alt="Starbie project" src="https://github.com/user-attachments/assets/57240d31-14cc-4566-b902-7402a9034963" />

# Starbie

Starbie is a tiny motion-controlled digital pet, inspired by a desktop Tamagotchi. It is a custom electronics project made for Hack Club's Half Life, built around a Seeed XIAO ESP32-C3, a small OLED display, physical buttons, and motion sensing.

The goal is to care for a little pixel pet using a simple on-device menu and movement gestures.

## What I made

- Designed a custom Starbie PCB in KiCad.
- Built the project around a Seeed XIAO ESP32-C3.
- Added a 128×64 SSD1306 I²C OLED display.
- Integrated an MPU6050 accelerometer and gyroscope to detect tilting and shaking.
- Added a DHT11 temperature and humidity sensor.
- Programmed a pixel pet with animations and three care stats: joy, energy, and fullness.
- Added a tilt-controlled radial menu and saved pet stats between restarts.

## Controls

| Control | Action |
| --- | --- |
| **Button 1 (XIAO D2 / GPIO4)** | On the pet screen, opens the radial menu. In the menu, confirms the action currently selected by tilting the device. |
| **Button 2 (XIAO D3 / GPIO5)** | Shows or hides the stats screen. It does not change the pet's stats. |
| **Tilt the device (MPU6050)** | While the radial menu is open, moves the selector to an action. Tilt up for **NAP**, right for **PLAY**, down for **FEED**, and left for **PET**. |
| **Shake the device (MPU6050)** | Gives the pet a small joy boost, with a small energy and fullness cost. A shake also wakes the pet from a nap. |

### Radial menu actions

| Direction | Action | Effect |
| --- | --- | --- |
| Up | **NAP** | The pet sleeps for 48 seconds and regains energy. |
| Right | **PLAY** | The pet runs around and gains joy, while using energy and fullness. |
| Down | **FEED** | The pet jumps and regains fullness. |
| Left | **PET** | The pet jumps and shows hearts, increasing joy. |

The pet's joy, energy, and fullness values range from 0 to 100. They change when you choose an action or shake Starbie; they do not automatically drain while the device is idle. Values are saved in the ESP32-C3's non-volatile preferences, so they persist after restarting.

## Hardware and pinout

The firmware uses these XIAO ESP32-C3 pins:

| Component / signal | XIAO pin | ESP32-C3 GPIO |
| --- | --- | ---: |
| OLED SDA | D4 | GPIO6 |
| MPU6050 SDA | D4 | GPIO6 |
| OLED SCL | D5 | GPIO7 |
| MPU6050 SCL | D5 | GPIO7 |
| DHT11 data | D1 | GPIO3 |
| Button 1 | D2 | GPIO4 |
| Button 2 | D3 | GPIO5 |

The OLED and MPU6050 share the I²C bus. The firmware expects the OLED at address `0x3C` and the MPU6050 at `0x68` by default. These can be changed in the beginner settings near the top of the sketch if the actual modules use different addresses.

## Firmware

The Arduino sketch is currently stored at the repository root as `Starbie.ino`.

### Requirements

- Arduino IDE
- ESP32 board support for the Seeed XIAO ESP32-C3
- Adafruit GFX Library
- Adafruit SSD1306
- Adafruit MPU6050
- DHT sensor library

Install the libraries through **Sketch → Include Library → Manage Libraries** in Arduino IDE. Install any additional dependencies that the IDE offers.

### Uploading the firmware

1. Open `Starbie.ino` in Arduino IDE.
2. Install the required libraries listed above.
3. Select the Seeed XIAO ESP32-C3 board and its connected serial port.
4. Connect the board over USB.
5. Click **Upload**.
6. After uploading, check that the OLED, buttons, and sensors respond as expected.

Most settings intended for customization are grouped near the top of the sketch under **BEGINNER SETTINGS**, including pin assignments, sensor use, starting stats, motion sensitivity, and menu direction.

If your build does not include a DHT11, set `USE_DHT11` to `false` in the sketch before uploading.

## Bill of Materials (BOM)

The table below lists the main parts for Starbie. Quantities and exact footprints should be checked against the latest schematic and PCB before purchasing or manufacturing.

| Qty. | Part | Purpose / specification |
| ---: | --- | --- |
| 1 | Seeed XIAO ESP32-C3 | Main microcontroller |
| 1 | SSD1306 OLED display, 128×64, I²C | Displays the pet, menu, and stats |
| 1 | MPU6050 module | Accelerometer and gyroscope for tilt and shake input |
| 1 | DHT11 sensor/module | Temperature and relative humidity; optional in firmware |
| 1 | 10 kΩ resistor | Include the exact reference and purpose from the final schematic |
| 2 | MX-compatible mechanical switches | Must match the MX footprints on the PCB |
| 2 | Compatible keycaps | Must fit the selected switch stems |
| 1 | Custom Starbie PCB | Designed in KiCad |
| As needed | Headers / connectors | For connecting modules and other parts, as required by the schematic |

### Switch compatibility

The original BOM listed 6×6 mm tactile buttons, but those do not fit the MX switch footprints used in the PCB. Replace them with mechanical switches that match the exact footprint and pin layout in KiCad. Check whether the footprint is for a 3-pin or 5-pin switch and confirm dimensions before ordering. Select keycaps that fit the chosen switches.

### BOM notes

The repository's generated `BOM.csv` currently lists the XIAO ESP32-C3, OLED, 6×6 mm tactile buttons, headers, and DHT11. The MPU6050, 10 kΩ resistor, PCB, and keycaps should also be represented in the final BOM, and the incompatible tactile-button entry should be updated to the selected MX-compatible switches. Update quantities and part links once the final schematic and selected parts are confirmed.

## Project files

- `Starbi.kicad_pro` — KiCad project
- `Starbi.kicad_sch` — schematic
- `Starbi.kicad_pcb` — PCB layout
- `Starbie.ino` — Arduino firmware
- `BOM.csv` — parts list

