/*
 * main_continuous contains the high-level state machine
 * with all the functions required for S-PAVe to park.
 * Functions include: reverse, park, and wiggle
 * Tasks include: Mario, Mario2
 * Main() task: The actual state machine
 * NOTE: all other main() methods need to be commented out to function properly
 *
 */


/*******************
* GLOBAL CONSTANTS *
*******************/

// Defines the dimensions of the car (in cm)
#define CAR_LENGTH 30
#define CAR_WIDTH 18
#define TURNING_RADIUS 4
#define SENSOR_OFFSET 2 // For wiggle, the sensors cannot be placed together

// Defines the parking spot
#define HEAD_IN_DEPTH 32
#define HEAD_IN_WIDTH 28
#define PARALLEL_DEPTH 22
#define PARALLEL_LENGTH  36
#define CONCRETE_WIDTH 8

// Constants for calculation
#define ERROR 2
#define PI 3

// Defines the goal of S-PAVe
#define HEAD_IN_PARK 0
#define PARALLEL_PARK 1

// STATES
#define LOOKING 0
#define DETECTING 1
#define ALIGNMENT 2
#define PARK 3
#define STOP 4
#define RESET 5


/*******************
* GLOBAL VARIABLES *
********************/
// condition variable
bool flag = false;

/**********************
* FUNCTIONS AND TASKS *
**********************/
// Starts the Mario theme song
task Mario();

// Starts the Flag-grabbing Mario theme song (Victory song)
task Mario2();

/* 
 * Used in state ALIGNMENT.
 * The reverse function is the half S-turn for HEAD_IN.  It is modularized
 * so that the function can be called multiple times and still perform
 * the same funcitonality.  This helps with each atomized time step.
 */
void reverse(int reverseDistance, int distance_remembered);

/*
 * Used in state PARK
 * The park function is both the S-turn for PARALLEL and full turn for HEAD_IN. 
 * This is also modularized to allow for multiple calls, but still maintain same
 * functionality.
 */
void park(bool headOrParallel, int parkDistance);

/*
 * Used in state STOP
 * The wiggle function performs the parking adjustments, which aligns the vehicle 
 * parallel to the right most surface.  This uses two ultrasonic sensors to determine
 * whether the front or rear of the car is misaligned.  Then by the conditions set,
 * the vehicle will realign itself along with the use of the bump sensors to maintain
 * ideal alignment.
 */
void wiggle(int distance, bool state, int RIGHT, int FRONT);

/*
 * used in state STOP
 * The clean_up function simply realigns the car if the front of the car is too far
 * to the front.  Uses the front touch sensor.
 */
void clean_up();


/*
 * task main().
 *
 * This is the main function, which performs all the necessary code for S-PAVe to run
 * as an integrated system.  Overall, it begins in state LOOKING to look for a potential
 * spot.  A spot is then validated in DETECTING, to detect any obstacles and open space.
 * After a spot is successfully characterized, the ALIGNMENT state positions the car in
 * the optimal location.  The PARK state helps to place/park the vehicle into the characterized
 * parking spot.  Finally, the STOP state stops the parking, and realigns the car optimally.
 * The state RESET is the kill-switch, finished parking, finally done state.
 *
 * Uses turnWheelsTo(int angle)
 *      drive(int distance)
 * from DrivingControl_continuous.nxc
 *
 * Uses InitBase()
 *      Sensys
 *	Touchsys
 * from Sensys.nxc
 */
task main();

/*********************************
* GLOBAL VARIABLES within main() *
*********************************/
// default state
int state = LOOKING;

// parameter to define whether parallel/head-in parking
bool isParallel = HEAD_IN_PARK;


// distance incremented in state DETECTING
int distance_remembered = 0;

// distance incremented in state ALIGNMENT
int distance_reversing = 0;

// distance incremented in state PARK
int park_distance = 0;

// maintains the distance from the right
int drop = 0;

// initial counter to offset the first few cycles for
// sensors to initialize
int count = 0;