# VORON SWITCHWIRE
## This is a Conversion **and** few Upgrades to VSW, for those who has 2020 and 2040 Aluminum Extrusion Profile.

![alt text](https://github.com/kanawati975/Voron_Switchwire/blob/main/Images/IMG_0046.jpeg)

All of this Repo contents are related to the Voron Switchwire and conversions/Mods. 

## Features and Specifications of my VSW
My Switchwire is a conversion from Geeetech A30 Printer, which is almost identical to the 12V good old Creality CR-10, built with 2020 and 2040 Aluminum Extrusion Profiles. What makes it special is:
- Automated Remote Power Control (via Relays, controlled by the Raspberry Pi from the GUI)
- Dual linear Rails with four MGN12H Blocks on the Y Axis.
- Maximum print Volume: 305 x 305 x 350 mm.
- Controller Board BTT SKR-2 at 168MHz.
- Raspberry Pi 3B Rev 1.2
- TMC2130 Silent Drivers on ~~all axis~~ the extruder. All other Axis are driven by Closed-Loop-System. 
- ~~Galileo~~ Clockwork 2 Extruder (Direct Drive).
- ~~Volcano Hotend~~ Standard V6 Nozzle with Ceramic rounded Heater Cartridge.
- 220VAC 750W 310x310 mm Silicone heated Bed (via SSR).
- 310 x 310 mm Heated Build Platform, with a magnetic Spring steel Sheet.
- Auto Bed (mesh) Probing... Well inslated Metal Detection Sensor/Z Probe.
- ~~Filament Rounout Sensor~~.
- Hybrid Chamber Temperature Control (Passive Heating + Active Chamber Cooling + Chamber Temperature Sensor).
- Custom 3D Printed skirt, with dual 8015 silent Fans.
- External dual USB Ports for further connections to the Raspberry Pi.
- Dual Cameras (RaspiCam+USB Cam) for front **and** back view of the Print.

![alt text](https://github.com/kanawati975/Voron_Switchwire/blob/main/Images/IMG_0046.jpeg)
![alt text](https://github.com/kanawati975/Voron_Switchwire/blob/main/Images/IMG_0047.jpeg)
![alt text](https://github.com/kanawati975/Voron_Switchwire/blob/main/Images/IMG_0048.jpeg)
![alt text](https://github.com/kanawati975/Voron_Switchwire/blob/main/Images/IMG_0049.jpeg)
![alt text](https://github.com/kanawati975/Voron_Switchwire/blob/main/Images/IMG_0050.jpeg)


## What's in this Repository?
[**- BL-Touch Mod**](https://github.com/kanawati975/Voron_Switchwire/tree/main/BL-Touch)

![alt text](https://github.com/kanawati975/Voron_Switchwire/blob/main/Images/bltouch.jpg)


[**- Emergency Mount**](https://github.com/kanawati975/Voron_Switchwire/tree/main/Emergency%20Mount/STL)

![alt text](https://github.com/kanawati975/Voron_Switchwire/blob/main/Images/emount.jpeg)


[**- Counterweight Key-Bak Alternative**](https://github.com/kanawati975/Voron_Switchwire/tree/main/Key-Bak)

![alt text](https://github.com/kanawati975/Voron_Switchwire/blob/main/Images/kbk.jpg)


[**- Raspberry pi Camera Mount**](https://github.com/kanawati975/Voron_Switchwire/tree/main/Pi-Cam)

![alt text](https://github.com/kanawati975/Voron_Switchwire/blob/main/Images/cammount.jpg)

[**- How to install Samba, to access your Pi's contents (Klipper directory) from Windows Explorer.**](https://github.com/kanawati975/Voron_Switchwire/blob/main/Samba/How%20to%20install%20samba.txt)
![alt text](https://github.com/kanawati975/Voron_Switchwire/blob/main/Images/smb.JPG)

[**- Sample configuration for Klipper on SKR-2 Controller Board**](https://github.com/kanawati975/Voron_Switchwire/tree/main/configuration/Klipper)

[**- Sample configuration for Marlin on SKR-2 Controller Board**](https://github.com/kanawati975/Voron_Switchwire/tree/main/configuration/Marlin)

# CONVERSION MODS:
[**- X/Z Motors Mount for the 2020 and 2040 Aluminum Extrusion Profile**](https://github.com/kanawati975/Voron_Switchwire/tree/main/Motor%20Mount)

[**- Upper Belt path / X and Z Blocks**](https://github.com/kanawati975/Voron_Switchwire/tree/main/Upper_XZ_Blocks)

[**- Modified Toolhead for the E3D Volcano**](https://github.com/kanawati975/Voron_Switchwire/tree/main/Volcano_Toolhead)

[**- Modified X Gantry Blocks/Carriers**](https://github.com/kanawati975/Voron_Switchwire/tree/main/XY_Gantry_Blocks)

[**- Modified Headless Front Grill (AKA Skirt) with single Push Button**](https://github.com/kanawati975/Voron_Switchwire/tree/main/Headless%20Skirt)


# USEFUL MACROS:
A collection of the most used or most useful Macros. 
#### All credit goes to the creators of those Macros.

[**- Start Print**](https://github.com/kanawati975/Voron_Switchwire/blob/main/configuration/Klipper/Read.md#start_print)

[**- End Print**](https://github.com/kanawati975/Voron_Switchwire/blob/main/configuration/Klipper/Read.md#end_print)

[**- Prime Line**](https://github.com/kanawati975/Voron_Switchwire/blob/main/configuration/Klipper/Read.md#prime-line)

[**- Park Toolhead**](https://github.com/kanawati975/Voron_Switchwire/blob/main/configuration/Klipper/Read.md#park-toolhead)

[**- Bed Mesh Calibrate (AKA G29)**](https://github.com/kanawati975/Voron_Switchwire/blob/main/configuration/Klipper/Read.md#bed-probe--mesh-leveling)

[**- Cancel/Abort Print**](https://github.com/kanawati975/Voron_Switchwire/blob/main/configuration/Klipper/Read.md#cancel_print)
