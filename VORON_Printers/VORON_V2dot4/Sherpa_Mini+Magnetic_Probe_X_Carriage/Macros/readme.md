# Magnetic Microswitch Probe Macros

These set of macros have been written to be used with the new magnetic microswitch probe that is completely solderless. It is intended to replace your toolhead inductive probe and z_endstop, performing both of their functions. There are two macros: one for a magprobe dock located at the rear of the gantry and another for a magprobe dock located at a fixed location next to the bed (coming soon). It can also be used with the MORON Magprobe.

Some features of the macros are:
* Probe connection check at toolhead macros that are called (and can be called) at several intervals with other macros, that stops other macros from proceeding and displays error messages displayed when something goes wrong.
* Attaching and docking magprobe with parameters for dock location, safe zones and speeds that are easily set by the user at the beginning of the macro.
* Redefining key commands (Quad Gantry Level, Bed Mesh Calibrate, Z Tilt) that uses a probe to work with the magprobe, especially in attaching and detaching.
* A G32 macro that allows you to perform several commands such as quad gantry level and bed mesh consecutively without constantly attaching and docking the probe in between commands.

To add these macros into your printer.cfg, you can upload this .cfg file into the same directory as your printer.cfg and include it in there. This may help in organising your macros and configurations without overly increasing the number of lines in your printer.cfg that happens when you just copy and paste it in. First, upload `magprobe_macros.cfg` into your pi directory, usually located at `/home/pi/` or `/home/pi/klipper_config`. Then, in your printer.cfg, add the following line under your Macros section: `[include /home/pi/magprobe_macros.cfg]` or `[include /home/pi/klipper_config/magprobe_macros.cfg]`.

Using the magprobe does not mean simply uploading the macros config and running it immediately. There are a few things that you need to do; please read on carefully.

## Updating [stepper_z] And [probe] Settings

