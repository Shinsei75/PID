# PID
Library of the classic PID controller

The PID controller accepts two values ​​as input:

input - signal from the sensor: temperature, speed, position, etc;
setpoint - the value to which the regulator will try to regulate the input signal (temperature, speed, position ...)
The output (control) signal output from the PID controller is a dimensionless quantity that is fed to the control device. It can be a PWM transistor, dimmer, servo, etc. The output signal should affect the input signal: the heater heats the object with the temperature sensor, the motor turns and gives values ​​for the speed sensor, etc.

The control law of the regulator is set using the coefficients Kp, Ki and Kd.

Kp - proportional factor, the output value will increase in proportion to the difference between the input signal and the setting.
Ki - the coefficient of the integrating component, is responsible for the accumulating error, allows you to smooth out ripples and level out a small error.
Kd - coefficient of the differential component, is responsible for the rate of change of the value, allows to reduce the buildup of the system.

