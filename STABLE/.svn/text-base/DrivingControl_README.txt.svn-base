 ----------------
|Global Variables|
 ----------------

odometer
Type: integer
Value: real-time value of how far the car has traveled since boot-up (only increases, even for distance traveled in reverse, just like odometers in real modern cars)

wheelAngle
Type: integer
Value: real-time value of the current (absolute) wheel angle (in degrees)

safe
type: boolean
Value: set to false if an overriding safety condition/concern exists, true otherwise; used to "interrupt" the functions below


 ---------
|Functions|
 ---------

bool drive(int distance)
------------------------
usage: drives the car a set distance (does not modify or care about wheel angle)
parameters: 
	distance: the amount to drive (in centimeters); positive value for forward, negative for reverse
modifies: odometer
returns: a boolean value indicating success (true), or false otherwise


bool turnWheelsTo(int desiredWheelAngle)
----------------------------------------
usage: turns the front wheels to a specific absolute angle (in degrees)
parameters: 
	wheelAngle: the desired wheel angle (in degress) (positive value for right turns, negative for left turns, but this can be changed via the preprocessor constants)
modifies: wheelAngle
returns: a boolean value indicating success (true), or false otherwise 



bool driveAndTurn(int distance, int endWheelAngle);    
---------------------------------------------------
usage: drive a specific distance while linearly changing the (absolute) wheel angle to endWheelAngle (in degrees)
parameters:
	distance: the total distance to drive (in centimeters)
	endWheelAngle: the desired wheel angle (in degress) desired at the end of the distance driven 
modifies: odometer, wheelAngle
returns: a boolean value indicating success (true), or false otherwise 


 ------------------------------------------------------------
|Selected Constants / settings || (type) NAME [values]: usage|
 ------------------------------------------------------------
*********Driving*********
(int) MOTOR_CONFIG [1/-1]: 1, if the driving motor is mounted forward; 1 if the driving motor is mounted backwards

(boolean) ODOMETER_REVERSE [true/false]: true, to have the odometer to turn back when the car drives in reverse; false, to have the odometer add the absolute value of the distance driven

(int) DRIVING_SAFETY_INCREMENT [0-???]: sets the amount of distance to drive in each iteration of a safety loop, the smaller the increment, the more opportunity for "interrupts" (using the "safe" flag)

*********Steering*********
(int) STEERING_CONFIG [1/-1]: if the motor is mounted so that "forward" turns the wheels to the right, and it is desired that positive wheel angles also correspond to turning to the right, use a value of 1;  otherwise, use a value of -1, and positive wheel angles will correspond to turning left.  OR, if the motor is mounted upside-down, and it is desired that positive wheel angles also correspond to turning to the right, use -1.  

