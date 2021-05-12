# Hibot Parameters
## Festo Servo/Stepper

![The param list of Cia402 moving protocal](http://gadgethi-css.s3.amazonaws.com/img_share/proj-008/param%20list%20of%20Cia402.png)

### Homing
* Homing Method: [ID type] The integer for setting the homing method. Now we suggest two homing methods which are listed below.


	17: Home on Negative Limit Switch
	18: Home on Positive Limit Switch

![Method 17](http://gadgethi-css.s3.amazonaws.com/img_share/proj-008/Homing%20Method%2017.png)

![Method 18](http://gadgethi-css.s3.amazonaws.com/img_share/proj-008/Homing%20Method%2018.png)

* Offset: [Int type] The offset length after the motor get home.
* Home Speed: [Int type] The velocity as the motor is homing. If the homing speed is too large, the motor may run over the sensor and won't stop there.
* Homing Acceleration: [Int type] The acceleration as the motor is homing.

### Moving
* Position Limit: [Int type] For protection. The upper limit of position.
* Profile Velocity: [Int type] The target velocity as moving the motor.
* Profile Acceleration: [Int type] The accleration as the motor speeds up to the profile velocity.
* Profile Deceleration: [Int type] The accleration as the motor speeds down to 0 from profile velocity.



## Festo IO Module
### CPX-AP-I-4AI-U-I-RTD-M12
* Signalrange: [ID type] Signal range, the choices are listed below

	0: no sensor connected (factory setting)
	1: –10 ... +10 V
	2: –5 ... +5 V
	3: 0 ... 10 V
	4: 1 ... 5 V
	5: 0 ... 20 mA
	6: 4 ... 20 mA
	7: resistance 0 ... 500 Ω
	8: PT100
	9: NI100  

* Temperature unit: [ID type] Unit for temperature measurement

	0: Celsius (factory setting)
	1: Fahrenheit
	2: Kelvin
	




