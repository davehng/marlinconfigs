# MK2.5S - BTT-002 - Hemera

Prusa MK2.5S printer with extruder changed to an E3D Hemera and Mini-Rambo changed to a BTT-002 with TMC2209 drivers.

As the printer is running on 12V, SpreadCycle mode on the TMC2209s is quite noisy (squealy). I've worked around this by using HYBRID_THRESHOLD so the drivers hold position in StealthChop and use SpreadCycle for all moves. The hybrid thresholds for each axis are set relatively low.

I'm not using sensorless homing on the TMC2209s as the MK2.5S has min limit switches, and i have FYSETC TMC2209 v2.0s which have the DIAG pin on a different pin to BTT's step sticks.

This configuration was based on the marlin config for MK3S/TMC2209 config by thisiskeithb & codiac2600.

The MK2.5S Hemera mount can be found [here](https://www.thingiverse.com/thing:4139915).
I've changed the probing margins so bed leveling doesn't crash into the right and back margins due to the Hemera positioning.

# Recommended PrusaSlicer Start G-Code
```gcode
G90 ; use absolute coordinates
M83 ; extruder relative mode
M104 S170 ; preheat extruder to 170
M140 S[first_layer_bed_temperature] ; set bed temp
M190 S[first_layer_bed_temperature] ; wait for bed temp
G28 ; home all
G29 ; mesh bed leveling
G1 X0 Z0.6 Y-3.0 F1000.0 ; go outside print area
M109 S[first_layer_temperature] ; wait for extruder temp
G92 E0.0
G1 X60.0 E9.0 F1000.0 ; intro line
G1 X120.0 E12.5 F1000.0 ; intro line
G92 E0.0
```