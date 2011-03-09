Bluetooth Connection:

blu_master.nxc should be installed on the controller
blu_slave.nxc should be installed on the actual car.

trickest part: establishing a connection between the two bricks.

Goals: 
1) Connect two NXT together
i. the "car" is the slave. Line 1
ii. the "control" is the master. Line 0
2) Send messages from control to car
i. Control is by buttons on the master controller
ii. Three controls to be used: center, left and right. exit button reserved for exiting the program
3) Simple GUI

Goals met.

STATES:
Two state: DRIVE and TURN
bool drive_state keeps track of the state
state transition: BTNCENTER (pressing the orange button in the center)
in DRIVE state: right button is go forward and left button is go backwards
in TURN state: right button is turn right and left button is turn left

 