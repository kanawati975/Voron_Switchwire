# Tips:

Here is some help about the configuration parameters, and some useful Macros. 
You can put them all together in printer.cfg file, or you can separate them in different files 
If you decided to make separate files, make sure to include ```file.name``` in the main printer.cfg file.
For macros, it's very common to add ```include macros.cfg``` in the printer config file.

## Useful Macros:
**Disclaimer:** I did not create the Macros. All credit goes to the creators.

## Park Toolhead:
This Macro is very useful and can be used with a lot of other macros, such as End_Print, Filament_Change, Cancel_Print, etc.
It will lift the Nozzle a little, to avoid collision, then moves to the right, and the bed will go forward.
```
[gcode_macro PARK_TOOLHEAD]
description: Script to park the ToolHead
gcode:
	 {% set x_park = printer.toolhead.axis_maximum.x|float - 5.0 %}
     {% set y_park = printer.toolhead.axis_maximum.y|float - 5.0 %}
     {% set max_z = printer.toolhead.axis_maximum.z|float %}
     {% set act_z = printer.toolhead.position.z|float %}
     {% if act_z < (max_z - 10) %}
       {% set z_safe = 2.0 %}
     {% else %}
       {% set z_safe = max_z - act_z %}
     {% endif %}
     G91
     G1 Z{z_safe +10} F900
     G90
     G0 X{x_park} Y{y_park} F6000
     G91
```
## Bed Probe / Mesh Leveling:
This macro will clear any previous mesh saved, and create a new mesh, then save it.
```
[gcode_macro G29]
gcode:
	G28			#Home All Axes
  G90
  BED_MESH_PROFILE REMOVE=default
  BED_MESH_PROFILE REMOVE=default_new
  BED_MESH_CLEAR
  BED_MESH_CALIBRATE
  BED_MESH_PROFILE SAVE=default_new
  SAVE_CONFIG
```

## Prime Line
This macro will create a line at the front of the bed. Basically it will prime the Nozzle and remove any excess Filament.
**Note:** Don't forget to add the Macro's Name to the Print_Start. If you want to customize the prime line, you can by adding the options to the Print_Start macro
```PRIME_LINE XPAD=10 YPAD=10 LENGTH=250 PRINT_SPEED=20 TRAVEL_SPEED=100 PURGE=15 RETRACT=1 EXTRUSION_MULTIPLIER=1.2 PRINT_HANDLE=1 HANDLE_FAN=100```

```
[gcode_macro PRIME_LINE]
description: Print an easy to remove parametric extruder priming line with a built-in handle.
gcode:
    # settings
    {% set line = {
      'x_padding'      : params.XPAD|default(10)|float,  # left/right padding around the bed the line can't print into
      'y_padding'      : params.YPAD|default(10)|float,  # top/bottom padding around the bed the line can't print into
      'initial_purge'  : params.PURGE|default(8)|int,   # mm of filament to purge before printing. set to 0 to disable
      'retract_after'  : params.RETRACT|default(1)|int, # mm of filament to recract after printing. set to 0 to disable
      'length'         : params.LENGTH|default(200)|int, # mm the length of the line
      'print_speed'    : params.PRINT_SPEED|default(20)|int,
      'travel_speed'   : params.TRAVEL_SPEED|default(100)|int,
      'extr_multi'     : params.EXTRUSION_MULTIPLIER|default(1.25)|float,  # apply to prime lines
      'overlap_percent': 80, # how much prime lines overlap each other
    } %}
    {% set handle = {
      'do_print'    : params.PRINT_HANDLE|default(1)|int,  # set to 0 to disable printing the handle
      'fan_percent' : params.HANDLE_FAN|default(100)|int,   # without fan the handle is too small and melty to print upright
      'width'       : 5.0,
      'height'      : 5.0,
      'move_away'   : 60   # how much to move the toolhead away from the printed handle once done. set 0 to disable
    } %}
    # sanity check and computed variables
    {% set max_x, max_y, nozzle_diameter = printer.toolhead.axis_maximum.x|float, printer.toolhead.axis_maximum.y|float, printer.configfile.config['extruder'].nozzle_diameter|float %}
    {% set _ = line.update({'width': nozzle_diameter * 1.25, 'height': nozzle_diameter / 2, 'length': [line.length, max_x - 2 * line.x_padding - 2]|min}) %}
    {% set _ = line.update({'e_per_mm': line.extr_multi * (line.width * line.height) / (3.1415 * (1.75/2)**2), 'x_start': max_x / 2 - line.length / 2, 'y_start': line.y_padding})  %}
    SAVE_GCODE_STATE NAME=STATE_PRIME_LINE
    M117 Prime Line
    G90 # absolute positioning
    G0 X{line.x_start} Y{line.y_start + (handle.width / 2)|int + 1} Z{line.height} F{line.travel_speed * 60} # move to starting position
    G91 # relative positioning
    G1 E{line.initial_purge} F{5 * 60} # extrude at ~12mm3/sec
    G0 F{line.print_speed * 60} # set print speed
    G1 X{line.length} E{line.length * line.e_per_mm} # print forward line
    G0 Y{line.width * line.overlap_percent / 100} # overlap forward line
    G1 X-{line.length / 2} E{(line.length / 2) * line.e_per_mm}  # print backward line for half the length
    # print a handle for easy removal
    {% if handle.do_print != 0 and handle.width != 0 and handle.height != 0 %}
      G0 X{handle.width} Y{handle.width / 2} # move into position for printing handle
      {% set saved_fan_speed = (printer['fan'].speed * 256)|int %}
      M106 S{((handle.fan_percent / 100) * 256)|int} # set part fan to desired speed
      {% for _ in range((line.height * 1000)|int, (handle.height * 1000)|int, (line.height * 1000)|int) %} # loop however many cycles it takes to print required handle height
        G1 Y{loop.cycle(-1.0, 1.0) * handle.width} E{handle.width * line.e_per_mm} # handle layer
        G0 X-{line.width * 0.2} Z{line.height} # move up and shift the layer to make the handle sloping
      {% endfor %}
      M106 S{saved_fan_speed} # restore previous part fan speed
    {% endif %}
    G1 E-{line.retract_after} F{50 * 60} # retract ar 50mm/sec after printing
    G0 Y{handle.move_away} F{line.travel_speed * 60}
    M117
    RESTORE_GCODE_STATE NAME=STATE_PRIME_LINE
```

