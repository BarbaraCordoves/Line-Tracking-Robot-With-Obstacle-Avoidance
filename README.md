# Line-Tracking-Robot-With-Obstacle-Avoidance
Autonomous navigation and control system for the Pioneer P3DX mobile robot, developed in Lua for CoppeliaSim. Implements a robust FSM for black-line tracking and dynamic, multi-state obstacle avoidance using IR and Ultrasonic sensors.

Control Logic & State Machine: The core intelligence resides in the sysCall_actuation() function, which defines a Finite State Machine (FSM) using the avoidanceState variable to manage the robot's complex behavior transitions.

The robot cycles through these states:

State 0: Normal Line Following

The default state. The robot uses the IR sensors to follow the black line. It remains here until one of the front ultrasonic sensors detects an obstacle within the target distance.
State 1: Initial Turn (Left)

Triggered immediately upon obstacle detection. The robot executes a sharp left turn to begin moving around the obstacle.
State 2: Go Straight

After the initial turn, the robot drives straight for a fixed duration (goStraightDuration). This maneuver ensures the robot has moved far enough past the obstacle's frontal plane.
State 3: Wall Following / P-Control

The robot uses the right ultrasonic sensor to maintain a safe, proportional distance from the obstacle/wall. It continuously checks for the black line's reappearance using the Middle IR Sensor.
State 4: Turn Back (Right)

Once the line is successfully re-acquired, the robot executes a controlled right turn for a set duration (turnRightDuration). This maneuver positions the robot back over the black line, completing the avoidance routine and returning the system to State 0.
The blacklineState variable is used to ensure the dedicated line-following logic is active only when the robot is not currently executing an obstacle avoidance maneuver.

System Components & Sensors: The system relies on data from two main sensor types: Vision Sensors (IR)—including left, middle, and right—are the primary input for line-tracking. Proximity Sensors (Ultrasonic)—specifically the front-facing and right-side units—are used for dynamic obstacle detection and wall-following. The Pioneer P3DX platform's Differential Drive Motors actuate movement based on the calculated wheel velocities.
