# SV04-KlipperConfigs
My klipper configs for sv04

## Software Edits
These should hopefully be drag and drop with minimal customizations if you have klipper, moonraker, KAMP and fluidd installed already, if not install the main KAMP directory as follows & follow other installation instructions

```
cd

git clone https://github.com/kyleisah/Klipper-Adaptive-Meshing-Purging.git

ln -s ~/Klipper-Adaptive-Meshing-Purging/Configuration printer_data/config/KAMP
```

## Hardware Edits
1. Only one simple hardware mod is required, in each extruders breakout board move the heatbreak fan connector over from the fixed fan1 slot over to the free K-fan plug. This allows percentage control of the heatbreak fan and switching it off when extruder is not in use.
   
## Config edits

1. Update "serial: /dev/serial/by-id/yourid" in printer.cfg to your printers serial port
2. Adjust your second extuders offset under the T1 macro in macros.cfg ('SET_GCODE_OFFSET Y=15') - you'll have to calibrate this after getting the printer setup for accurate dual colour printing
3. in fluidd.cfg set virtual_sdcard path to your gcode files path.

## Slicer edits
For the slicer setup I use prusaslicer (have started converting to orca but not done yet) and have 4 Physical printers setup, SV04 Main, SV04 Dual, SV04 Mirror and SV04 copy in order to coordinate what I want the printer to do
### Global
End G-code
```
END_PRINT
```

### Dual Mode
Start G-code
```
G28 X 
SET_DUAL_CARRIAGE CARRIAGE=0 MODE=PRIMARY 
START_PRINT EXTRUDER=[current_extruder] EXTRUDERS=2 EXTRUDER_TEMP={first_layer_temperature[0]} EXTRUDER1_TEMP={first_layer_temperature[1]} BED_TEMP={first_layer_bed_temperature[0]}
```
Tool change G-code
```
M104 S{temperature[next_extruder] - 10}
T{next_extruder}
M104 S{temperature[next_extruder]}
G4 S5
G1 E3 F300
```

### Copy Mode
Start G-code
```
G28 X 
ACTIVATE_COPY_MODE
START_PRINT EXTRUDER=[current_extruder] EXTRUDERS=2 EXTRUDER_TEMP={first_layer_temperature[0]} EXTRUDER1_TEMP={first_layer_temperature[1]} BED_TEMP={first_layer_bed_temperature[0]}
```

### Mirror Mode
Start G-code
```
G28 X 
SET_DUAL_CARRIAGE CARRIAGE=1 MODE=MIRROR 
START_PRINT EXTRUDER=[current_extruder] EXTRUDERS=2 EXTRUDER_TEMP={first_layer_temperature[0]} EXTRUDER1_TEMP={first_layer_temperature[1]} BED_TEMP={first_layer_bed_temperature[0]}
```

This is based off theory and memory of what needs to be changed as I have not tested this method on a clean sv04 install - these are simply the configs I use & from my knowledge of whats needs to be done. Errors may arrise from things ive missed but a simple google should provide you the fix.



