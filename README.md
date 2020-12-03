# PID
<h1 align="center">Library of the classic PID controller</h1>

### [Readme on russian](https://github.com/Shinsei75/README.ru)

## How this work.
The PID controller accepts two values ​​as input:

**input** - signal from the sensor: temperature, speed, position, etc;

**setpoint** - the value to which the regulator will try to regulate the input signal (temperature, speed, position ...)

The output (control) signal output from the PID controller is a dimensionless quantity that is fed to the control device. It can be a PWM transistor, dimmer, servo, etc. The output signal should affect the input signal: the heater heats the object with the temperature sensor, the motor turns and gives values ​​for the speed sensor, etc.

The control law of the regulator is set using the coefficients Kp, Ki and Kd.

Kp - proportional factor, the output value will increase in proportion to the difference between the input signal and the setting.
Ki - the coefficient of the integrating component, is responsible for the accumulating error, allows you to smooth out ripples and level out a small error.
Kd - coefficient of the differential component, is responsible for the rate of change of the value, allows to reduce the buildup of the system.

## Initialization
`PID regulator;` // initialize without settings (everything is zeros, dt 100 ms)

`PID regulator (kp, ki, kd);` // initialize with coefficients. dt will be default 100ms

`PID regulator (kp, ki, kd, dt);` // initialize with coefficients and dt (in milliseconds)

## Modes and settings

Control direction: depends on which direction the controlled value **input** is directed when the control signal **output** increases. For example: cooling or heating, acceleration or deceleration, etc. The default is **NORMAL** - the regulator considers that increasing the **output** control signal will increase the **input** signal. Installed by the command

`setDirection(foo);`  // foo – NORMAL or REVERSE

Operating mode: regulation mode by error of the input signal **ON_ERROR** or by changing the input signal **ON_RATE**. The default is **ON_ERROR**, it is recommended to use it in most cases, because most processes are self-adjusting (the heater temperature will set itself to its maximum, the motor speed will also). The **ON_RATE** mode is recommended for integration processes in which the output value affects the rate of change of the input value, for example, the position of a motorized slider that will not stop when a control signal is different from zero. This process will be easier to manage in **ON_RATE** mode. Installed by the command

`setMode(mode);` // mode – ON_ERROR or ON_RATE

Output Limits: Limit the output value, default: 0-255 (for 8 bit PWM). Can be set 0-180 for servo angle, etc. Installed by the command

`setLimits(min, max);`  // set limits

Iteration time: the iteration time can be changed in the process of work (I don't know why, but there is a possibility). The time is set in milliseconds and affects the `getResultTimer ()` function, which makes a new calculation of the control signal with this period. Also, this time is included in the calculation of the control signal (in the I and D component). Installed by the command

`setDt(dt);`  // setting the iteration time in ms

## Setting / reading parameters

The main values of the regulator can be changed anywhere in the program in any convenient way (buttons, encoder, transmission via UART / GSM / WiFi, whatever). The controller coefficients Kp, Ki and Kd can be set and read directly as class members, for example

`regulator.Kp = 1.5;`        // set

`regulator.Ki += 0.7;`       // change

`lcd.print(regulator.Kd);`   // read

The iteration time is changed using the `setDt ()` method.

Controller values (input, set, output) are also class members and can be accessed directly for reading and writing:

`regulator.input = 10;`     // Controller INPUT, e.g. current temperature

`regulator.setpoint = 20;`  // INSTALLATION of the controller, e.g. required temperature

`analogWrite(regulator.output);`  // The output from the regulator can be fed directly to the PWM or servo
