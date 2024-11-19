# SV04-KlipperConfigs
My klipper configs for sv04

These should hopefully be drag and drop with minimal customizations if you have klipper, moonraker, KAMP and fluidd installed already, if not install the main KAMP directory as follows & follow other installation instructions

```
cd

git clone https://github.com/kyleisah/Klipper-Adaptive-Meshing-Purging.git

ln -s ~/Klipper-Adaptive-Meshing-Purging/Configuration printer_data/config/KAMP
```

1. Only one simple hardware mod is required, in each extruders breakout board move the heatbreak fan connector over from the fixed fan1 slot over to the free K-fan plug. This allows percentage control of the heatbreak fan and switching it off when extruder is not in use.
2. Update "serial: /dev/serial/by-id/yourid" in printer.cfg to your printers serial port
3. Adjust your second extuders offset under the T1 macro in macros.cfg ('SET_GCODE_OFFSET Y=15') - you'll have to calibrate this after getting the printer setup for accurate dual colour printing
4. in fluidd.cfg set virtual_sdcard path to your gcode files path.

This is based off theory and memory of what needs to be changed as I have not tested this method on a clean sv04 install - these are simply the configs I use & from my knowledge of whats needs to be done. Errors may arrise from things ive missed but a simple google should provide you the fix.
