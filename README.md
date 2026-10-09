# Voron-2.4-Octopus-pro-1
Voron 2.4  Octopus pro 1

[include nighthawk.cfg]
[include ./Demon_Klipper_Essentials_Unified/*.cfg]
[include ./Demon_User_Files/*.cfg]
[include ./Demon_Klipper_Essentials_Unified/Other_Files/Demon_User_Files_Updater/Demon_User_Files_Handler_v*.cfg]
[include Heat_Soak.cfg]
[include ./KAMP_LiTE/*.cfg]

[include stealthburner_leds.cfg]
[include mainsail.cfg]
[include My_Macros.cfg]
[include shell_command.cfg]
[save_variables]
filename = ~/demon_vars.cfg

[force_move]
enable_force_move: True




[exclude_object]
[virtual_sdcard]
path: /home/voron24/printer_data/gcodes
on_error_gcode: CANCEL_PRINT

[mcu]
serial: /dev/serial/by-id/usb-Klipper_stm32f446xx_460023000E5053424E363620-if00
restart_method: command

[mcu nhk]
serial: /dev/serial/by-id/usb-Klipper_rp2040_4E363334320F825C-if00
restart_method: command
##--------------------------------------------------------------------

[printer]
kinematics: corexy
max_velocity: 300  
max_accel: 3000    			#Max 4000
max_z_velocity: 15 			#Max 15 for 12V TMC Drivers, can increase for 24V
max_z_accel: 350
square_corner_velocity: 5.0

[idle_timeout]
gcode:
    _DEMON_IDLE_TIMEOUT
timeout: 3600

#####################################################################
# 	X/Y Stepper Settings
#####################################################################

## X Stepper on MOTOR0(B Motor)
[stepper_x]
step_pin: PF13
dir_pin: PF12
enable_pin: !PF14
rotation_distance: 40
microsteps: 16
full_steps_per_rotation:200  #set to 400 for 0.9 degree stepper
endstop_pin: nhk:gpio13
position_min: -4
position_endstop: 352
position_max: 352
homing_speed: 100
homing_retract_dist: 5
homing_positive_dir: true

[tmc2209 stepper_x]
uart_pin: PC4
interpolate: True
run_current: 0.8
hold_current: 0.7
sense_resistor: 0.110
stealthchop_threshold: 0

## Y Stepper on MOTOR1 (A Motor)
[stepper_y]
step_pin: PG0
dir_pin: PG1
enable_pin: !PF15
rotation_distance: 40
microsteps: 16
full_steps_per_rotation:200  #set to 400 for 0.9 degree stepper
endstop_pin: PG9
position_min: -6
position_endstop: 350
position_max: 350
homing_speed: 100
homing_retract_dist: 5
homing_positive_dir: true

##	Make sure to update below for your relevant driver (2208 or 2209)
[tmc2209 stepper_y]
uart_pin: PD11
interpolate: True
run_current: 0.8
hold_current: 0.7
sense_resistor: 0.110
stealthchop_threshold: 0
 
#####################################################################
# 	Z Stepper Settings
#####################################################################

## Z0 Stepper - Front Left on MOTOR2_1
[stepper_z]
step_pin: PF11
dir_pin: PG3
enable_pin: !PG5
rotation_distance: 40
gear_ratio: 80:16
microsteps: 16
endstop_pin: probe:z_virtual_endstop
position_max: 340
position_min: -5
homing_speed: 8
second_homing_speed: 3
homing_retract_dist: 0

##	Make sure to update below for your relevant driver (2208 or 2209)
[tmc2209 stepper_z]
uart_pin: PC6
interpolate: true
run_current: 0.8
hold_current: 0.8
sense_resistor: 0.110
stealthchop_threshold: 0

##	Z1 Stepper - Rear Left on MOTOR3
[stepper_z1]
step_pin: PE2
dir_pin: !PE3
enable_pin: !PD4
rotation_distance: 40
gear_ratio: 80:16
microsteps: 16

##	Make sure to update below for your relevant driver (2208 or 2209)
[tmc2209 stepper_z1]
uart_pin: PE1
interpolate: true
run_current: 0.8
hold_current: 0.8
sense_resistor: 0.110
stealthchop_threshold: 0

##	Z2 Stepper - Rear Right on MOTOR4
[stepper_z2]
step_pin: !PF9
dir_pin: PF10
enable_pin: !PG2
rotation_distance: 40
gear_ratio: 80:16
microsteps: 16

##	Make sure to update below for your relevant driver (2208 or 2209)
[tmc2209 stepper_z2]
uart_pin: PF2
interpolate: true
run_current: 0.8
hold_current: 0.80
sense_resistor: 0.110
stealthchop_threshold: 0

##	Z3 Stepper - Front Right on MOTOR5
[stepper_z3]
step_pin: PC13
dir_pin: !PF0
enable_pin: !PF1
rotation_distance: 40
gear_ratio: 80:16
microsteps: 16

##	Make sure to update below for your relevant driver (2208 or 2209)
[tmc2209 stepper_z3]
uart_pin: PE4
interpolate: true
run_current: 0.8
hold_current: 0.80
sense_resistor: 0.110
stealthchop_threshold: 0


#####################################################################
## 	                           Probe                               ##
#####################################################################

[beacon]
serial: /dev/serial/by-id/usb-Beacon_Beacon_RevH_110762BF5157355957202020FF0F113B-if00
x_offset: 0
y_offset: 23.8
mesh_main_direction: x
#mesh_runs: 2
lift_speed: 75
#is_non_critical: True
z_settling_time: 200
speed: 500
contact_max_hotend_temperature: 310
home_xy_position: 175,175
home_z_hop: 5
home_z_hop_speed: 30
home_xy_move_speed: 500
home_method: contact
home_method_when_homed: proximity
home_autocalibrate: unhomed
#mesh_overscan: 1

[resonance_tester]
accel_chip: beacon
probe_points: 175,175,20

#####################################################################
# 	Bed Heater
#####################################################################

[heater_bed]
##	SSR Pin - BED_OUT
heater_pin: PA3
sensor_type: Generic 3950
sensor_pin: PF3
##	Adjust Max Power so your heater doesn't warp your bed
max_power: 1
min_temp: 0
max_temp: 120
#control: pid
#pid_kp: 58.437
#pid_ki: 2.347
#pid_kd: 363.769

[extruder]
step_pin: nhk:gpio23
dir_pin: !nhk:gpio24
enable_pin: !nhk:gpio25
rotation_distance: 4.637
microsteps: 32
full_steps_per_rotation: 200
nozzle_diameter: 0.400
filament_diameter: 1.750
heater_pin: nhk:gpio9
#control: pid
#pid_Kp: 21.527
#pid_Ki: 1.063
#pid_Kd: 108.982
min_extrude_temp: 170
min_temp: 0
max_temp: 320
max_power: 1.0
sensor_type: PT1000
sensor_pin: nhk:gpio29
pullup_resistor: 2200
max_extrude_only_distance: 500
max_extrude_only_velocity: 120
max_extrude_cross_section: 5.0
pressure_advance_smooth_time: 0.02
pressure_advance: 0.025 
#pin: nhk:gpio10
#####################################################################
# 	Fan Control
#####################################################################

[heater_fan Hotend_fan]
pin: nhk:gpio5
heater: extruder
heater_temp: 40.0

[fan]
pin: nhk:gpio6

[heater_fan exhaust_fan]
pin: PE5
max_power: 1.0
shutdown_speed: 0.0
kick_start_time: 5.0
heater: heater_bed
heater_temp: 70
fan_speed: 1.0

[heater_fan DriverA]
pin: PD12
max_power: 1.0
shutdown_speed: 1.0
cycle_time: 0.0001     #10 kHz PWM signal
hardware_pwm: False
kick_start_time: 0
fan_speed: 0.9
heater: heater_bed
heater_temp: 45.0

[heater_fan Driver]
pin: PD14
max_power: 1.0
shutdown_speed: 1.0
cycle_time: 0.0001     #10 kHz PWM signal
hardware_pwm: False
kick_start_time: 0
fan_speed: 0.9
heater: heater_bed
heater_temp: 45.0

[temperature_sensor Chamber]
sensor_type: PT1000
sensor_pin: PF4
min_temp: 0
max_temp: 250
gcode_id: chamber

[temperature_sensor RPI]
sensor_type: temperature_host

[temperature_sensor Octopus]
sensor_type: temperature_mcu

#####################################################################
# 	LED Control
#####################################################################

[led Printer_Lights]
white_pin: PB10
cycle_time: 0.0010
initial_WHITE: 1.0


#####################################################################
# 	Homing and Gantry Adjustment Routines
#####################################################################

[idle_timeout]
timeout: 1800

[quad_gantry_level]
gantry_corners:
  -60,-10
  410,420
points:
  25, 5
  25, 305
  325, 305
  325, 5
  #25, 25
  #25, 325
  #325, 325
  #325, 25
horizontal_move_z: 10
speed: 800
retries: 15
retry_tolerance: 0.003
max_adjust: 15
speed: 100
horizontal_move_z: 10
retries: 5
retry_tolerance: 0.0075
max_adjust: 10

[bed_mesh]
speed: 500
horizontal_move_z: 2
mesh_min: 20,25
mesh_max: 330 ,325
probe_count: 50, 50
fade_start: 0.5
fade_end: 10
algorithm: bicubic
zero_reference_position: 175, 175
split_delta_z: 0.0125
move_check_distance: 3
#mesh_pps: 2, 2
mesh_pps: 0,0
#bicubic_tension: 0.1


[delayed_gcode encoder_sensor]
initial_duration: 1
gcode:
    SET_FILAMENT_SENSOR SENSOR=encoder_sensor ENABLE=0
[filament_motion_sensor encoder_sensor]
switch_pin: PG13
detection_length: 9
extruder: extruder
pause_on_runout: False
insert_gcode:
    { action_respond_info("Filament Encoder is Running") }
runout_gcode:
    { action_respond_info("Filament Encoder Stall Detected") }
    {% if printer.print_stats.state == "printing" %}
      _FIL_CHANGE_PARK
    {% endif %}

[delayed_gcode encoder_sensor]
initial_duration: 1
gcode:
    SET_FILAMENT_SENSOR SENSOR=encoder_sensor ENABLE=0


########################################
# EXP1 / EXP2 (display) pins
########################################

[board_pins]
aliases:
    # EXP1 header
    EXP1_1=PE8, EXP1_2=PE7,
    EXP1_3=PE9, EXP1_4=PE10,
    EXP1_5=PE12, EXP1_6=PE13,    # Slot in the socket on this side
    EXP1_7=PE14, EXP1_8=PE15,
    EXP1_9=<GND>, EXP1_10=<5V>,

    # EXP2 header
    EXP2_1=PA6, EXP2_2=PA5,
    EXP2_3=PB1, EXP2_4=PA4,
    EXP2_5=PB2, EXP2_6=PA7,      # Slot in the socket on this side
    EXP2_7=PC15, EXP2_8=<RST>,
    EXP2_9=<GND>, EXP2_10=<5V>

#####################################################################
# 	Displays
#####################################################################


#####################################################################
# 	Macros
#####################################################################

[gcode_macro G32]
gcode:
    BED_MESH_CLEAR
    G28
    QUAD_GANTRY_LEVEL
    G28
    G0 X175 Y175 Z30 F3600

#*# <---------------------- SAVE_CONFIG ---------------------->
#*# DO NOT EDIT THIS BLOCK OR BELOW. The contents are auto-generated.
#*#
#*# [beacon model default]
#*# model_coef = 1.5016386662575685,
#*# 	  1.8326678460689234,
#*# 	  0.7796856031974753,
#*# 	  0.36012975125331925,
#*# 	  0.3247426975125784,
#*# 	  0.40787806466511933,
#*# 	  -0.0910087765021019,
#*# 	  -0.38028694702123195,
#*# 	  0.0844361410453511,
#*# 	  0.18167948955185761
#*# model_domain = 1.8386156022322283e-07,1.9282889857096052e-07
#*# model_range = 0.200000,5.000000
#*# model_temp = 44.475906
#*# model_offset = 0.00000
#*#
#*# [extruder]
#*# control = pid
#*# pid_kp = 35.649
#*# pid_ki = 8.802
#*# pid_kd = 36.095
#*#
#*# [heater_bed]
#*# control = pid
#*# pid_kp = 61.800
#*# pid_ki = 2.124
#*# pid_kd = 449.593
#*#
#*# [input_shaper]
#*# shaper_type_x = mzv
#*# shaper_freq_x = 75.2
#*# shaper_type_y = mzv
#*# shaper_freq_y = 39.8
