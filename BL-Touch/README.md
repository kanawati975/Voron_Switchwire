This is a Modification to the Afterburner's Tolhead, to accept the touch Sensor (AKA BL-Touch, 3D Touch, etc.)

![alt text](https://github.com/kanawati975/Voron_Switchwire/blob/main/BL-Touch/Screenshot%202021-11-01%20053315.jpg)

![alt text](https://github.com/kanawati975/Voron_Switchwire/blob/main/BL-Touch/IMG_4372.jpeg)

For this Mod you can use the two M3x10 screws. 
The M3x20 screws and the Probe Bracket are no longer needed.

![alt text](https://github.com/kanawati975/Voron_Switchwire/blob/main/BL-Touch/IMG_5097.jpeg)

It is highly recommened to use any available insulation material to reduce heat on the touch Sensor.

Here's my config senction. Please use it as reference.

```
[bltouch]
sensor_pin: ## Your sensor Pin
control_pin: ## Your data Pin
probe_with_touch_mode: true
pin_up_reports_not_triggered: true
pin_up_touch_mode_reports_triggered: true
stow_on_each_sample: False 
x_offset: 0.0
y_offset: -24
z_offset: 0
speed: 5
lift_speed: 1
samples: 1
sample_retract_dist: 10
samples_result: average
```
