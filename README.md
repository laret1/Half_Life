<img width="1277" height="855" alt="Captura de pantalla 2026-10-27 011342" src="https://github.com/user-attachments/assets/e801b92f-12bc-4d51-b2ff-e0bb30c89152" />
<img width="337" height="243" alt="Starbie project" src="https://github.com/user-attachments/assets/57240d31-14cc-4566-b902-7402a9034963" />

# Starbie 🐾

## What is Starbie?

Starbie is a little digital pet, kind of like a Tamagotchi. You have to take care of it, play with it, feed it and make sure it gets some rest is so interesant that tamagochi.

The idea behind this project was to make my own version of a digital pet, but also let other people build one themselves. It has a small screen, sensors and a custom PCB, so you can interact with your pet just by moving the device around i really dont know if it work so dont belive in me already.

## What I made

For this project, I designed the PCB in KiCad and worked on the firmware using Arduino IDE. I wanted Starbie to be more than just a screen with a character on it, so I added different ways to interact with the pet with buttons and that things.

Here is what I worked on:

- Designed a custom PCB using KiCad.
- Used a Seeed XIAO ESP32-C3 as the main microcontroller so the starbi have a brain.
- Added a 128x64 SSD1306 OLED screen to display the pet and its menus so you can see how adorable is.
- Added an MPU6050 to detect tilting and shaking so you can play better with him.
- Included a DHT11 sensor to read temperature and humidity so it have a lot of tecnologia.
- Made a radial menu controlled by tilting the device.
- Added a system to save the pet's stats, so they don't reset every time you turn it off because thats boring.

The firmware is written in Arduino C++ and the idea is to keep the project simple enough for other people to understand and modify.

 How to use it

Starbie has two buttons and an MPU6050 sensor. Most of the interactions are done through the buttons and by moving the device.

Each stat goes from 0 to 100. They change when you interact with Starbie, but they don't automatically decrease while the device is doing nothing.

I also made the stats save to the ESP32-C3's internal non-volatile storage. This means your pet keeps its stats even after restarting the device.

## Hardware and pinout

The project uses a Seeed XIAO ESP32-C3 and a few external modules connected to the custom PCB this is a lot of tecnical things so it was difficult.

| Component | XIAO pin | GPIO |
| --- | --- | --- |
| OLED SDA | D4 | GPIO6 |
| MPU6050 SDA | D4 | GPIO6 |
| OLED SCL | D5 | GPIO7 |
| MPU6050 SCL | D5 | GPIO7 |
| DHT11 data | D1 | GPIO3 |
| Button 1 | D2 | GPIO4 |
| Button 2 | D3 | GPIO5 |




 Software

The firmware is in `Starbie.ino` at the root of the repository.

To work on the project, you will need:

- Arduino IDE
- ESP32 board support for the Seeed XIAO ESP32-C3
- Adafruit GFX Library
- Adafruit SSD1306
- Adafruit MPU6050
- DHT sensor library
else you cant give starbi life
You can install the libraries through **Sketch → Include Library → Manage Libraries** in Arduino IDE. Some libraries may install additional dependencies, so make sure to install those too or you starbi will be sad.

### Uploading the firmware

1. Open `Starbie.ino` in Arduino IDE.
2. Install the required libraries.
3. Connect the XIAO ESP32-C3 to your computer using USB.
4. Select the correct board and serial port.
5. Upload the code.
6. Check that the screen, buttons and sensors are working.

and the starbi is ready to play with you

## Bill of Materials (BOM)

These are the main components used for Starbie. Some parts may depend on the final PCB version, so check the schematic and footprints before ordering anything or you starbi will be incompleted.

| Qty. | Component | Purpose |
| --- | --- | --- |
| 1 | Seeed XIAO ESP32-C3 | Main microcontroller |
| 1 | SSD1306 OLED 128x64 (I2C) | Displays the pet, menus and stats |
| 1 | MPU6050 module | Detects movement, tilting and shaking |
| 1 | DHT11 sensor/module | Measures temperature and humidity |
| 1 | 10kΩ resistor | Used by the circuit; check the final schematic for its exact purpose |
| 2 | MX-compatible mechanical switches | Physical buttons |
| 2 | Compatible keycaps | Used with the mechanical switches |
| 1 | Custom PCB | The board designed in KiCad |
| As needed | Headers and connectors | Connect the modules and other components |


## Project files

Here are the main files included in the repository:

- `Starbi.kicad_pro` — KiCad project settings.
- `Starbi.kicad_sch` — Circuit schematic.
- `Starbi.kicad_pcb` — PCB layout.
- `Starbie.ino` — Arduino firmware.
- `BOM.csv` — Bill of Materials.


If you build your own Starbie or make changes to the project, feel free to experiment with it!
