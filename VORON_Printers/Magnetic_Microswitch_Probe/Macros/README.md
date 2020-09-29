# Magnetic Microswitch Probe Homing Macros

Presently klipper does not support movement of the Z axis for the probe 
activate and probe deactivate gcode. This makes it somewhat problematic 
to attach a probe. Additionally, without some sort of state management, 
the probe will repeatedly attach and dock after every operation. These 
macros maintain probe attachment throughout operations.

You will want to comment out any safe_z_home or homing_override you may 
already be using. Any macros that override any of the Z axis calibration 
routines such as bed_mesh, bed_tilt, and quad_gantry_level should be 
commented out as well.

To utilize these macros, either copy and paste the contents of the macro file 
into your existing config or create a new file and an include line in 
your printer.cfg file.

There are several variables at the top of the file that should be configured
prior to running any of these macros. As always, keep your hand on the 
estop when running these for the first time (and some subsequent runs) 
just to be sure they are working as intended.

The default behavior is to require X and Y to be homed before homing 
the Z axis. If the probe is being used as the Z endstop, the macros
will home off the center of the bed. If there is a physical endstop
in use, it will either home over the specified coordinates (Voron
Z Endstop). In the case of a printer with a rigid, fixed endstop on
the axis itself, the printer will just home off that.


    variable_estop_probe_failure:   False

Setting this value to true will cause the macro to execute an M112 shutdown
in the event of a probe failure.

    variable_dock_x:                300
    variable_dock_y:                295
    variable_dock_z:                20
    
The absolute coordinates of the location of the probe dock. When setting
them, you should line the tool up with the probe on the X axis and then
advance the tool along the Y axis until the magnets attract.     
    
    variable_travel_speed:          100
    variable_dock_speed:            30
    
Travel speeds are the speeds used for non-probing and non-docking moves.
Docking speed is the speed the tool will move while it is docking and
attaching the probe. It should be relatively slow.

    variable_z_endstop_x:            0
    variable_z_endstop_y:            0
   
The macros will automatically determine what type of homing to do on
the Z axis based on the endstop pin definition for the Z stepper motors.
Some printers like the K2 and Voron have Z endstop switches located 
somewhere in the build envelope. The coordinates of this switch should
be supplied here. Printers like the I3 have physical endstops mounted
to the frame and do not require a location to be specified so these
values should be left as 0. If the probe is being used to home the Z
axis, these values should be left as 0.
   
    variable_park_toolhead:         True
    
After a G28 on all 3 axes, if this is set to True, the toohead will
move to a parking location after the homing and final calibrations
have been completed.

    variable_parkposition_x:        150   
    variable_parkposition_y:        20      
    variable_parkposition_z:        50   
    
These variables specify the position to park the toolhead after homing.

    variable_enable_z_calibration:  True
    variable_enable_mesh:           True

After the Z axis is intially homed, if Z calibration is enabled and 
a Z axis calibration routine is specified in the config file, it will
be run. Z axis calibration routines include, Quad Gantry Level, Bed Tilt,
and Z Tilt. If bed meshing is configured and the mesh option is True, it 
will run a bed mesh after Z calibration.

    variable_always_mesh:           False   
    variable_always_z_calibrate:    False  

By default, after the Z axis is homed and calibrated, subsequent requests
to home the Z axis will not cause calibration to be re-run. Changing these
options to True will force calibration after every Z homing operation.

# 09-28-2020

Initial commit of homing macros. 

