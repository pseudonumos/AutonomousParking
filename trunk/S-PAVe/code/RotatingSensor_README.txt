 ----------------
|Global Variables|
 ----------------
rotatableSensorPosition
TYPE: integer
VALUE:
	FACING_LEFT 0  	Sensor is facing to the left
	FACING_BACK 1  	Sensor is facing back
	SWEEPING 2  	Sensor is in a sweeping mode: sweeping from back to left, and left to back, CONSTANTLY
	ROTATING -1  	Sensor is in the process of turning from back to left, or left to back, BUT IS NOT SWEEPING


sweep
TYPE: bool
VALUE: flag to "interrupt" the rotateSensor() function to stop it from sweeping the sensor



 ---------
|Functions|
 ---------

bool rotateSensor(int desiredPosition)
--------------------------------------
USAGE: rotates a sensor to a desired position, or makes it constantly sweep. 
PARAMETERS:
	desiredPosition: the desired position of the sensor (can be: FACING_LEFT, FACING_BACK, or SWEEPING)
MODIFIES: rotatableSensorPosition
RETURNS: a boolean value indicating success (true), or false otherwise
NOTE: "sweep" (the global variable described above) is strictly a flag that rotateSensor() will check/read so it knows when to stop; rotateSensor() will not write to it to indicate that it has stopped sweeping. It is up to the calling function to reset this flag. 
