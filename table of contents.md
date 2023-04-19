1. [[1. electrical components]]
	1. [[1. electrical components#Motors]]
	3. [[1. electrical components#Encoders]]
	4. pneumatics: solenoids should be triggered only briefly to avoid burning out
	5. [[1. electrical components#Switch]]
	6. [[1. electrical components#misc sensors]]
	7. accelerometer
	8. [[1. electrical components#Gryoscopes]]
2. [[2. intro computers and programs]]
	1. computers on the robot
	2. binary and data storage
	3. intro boolean algebra
	4. [[2. intro computers and programs#BASIC programming (literally)]]
	5. [[2. intro computers and programs#how computers think]]
4. workflows for software development and how to integrate it into the hardware lifecycle
	1. basic git (using visual git client like github desktop or vscode)
	2. basic git workflow
	3. how to prioritize and create issues (including boards).
	4. reviewing and **testing** code
5. intro control systems
	1.  https://en.wikipedia.org/wiki/Control_system
	2. open vs closed loop
	3. explain how a thermostat uses bang bang control for a closed loop system
	4. give examples of closed loop and open loop systems using the robot components we went over earlier
	5. how we might want to go about controlling a motor using psudocode. explain concepts like how a loop works (program a thermostat in this example using the sensor to explain how timing works and relate specifically to robot code timings like the periodic loops)
	6. explain debouncing and basics of digital signal processing with examples of noisy sensor data.
6. basic java
	1. explain java programming concepts
		- https://www.youtube.com/watch?v=GoXwIVyNvX0 (entire video; though the private/public chatter isn't really great)
		- data types https://www.youtube.com/watch?v=6otW6OXjR8c (only first 3 mins)
		- basic syntax
		- basic logic statements
		- object oriented code
7. command based programming
	1. subsystems
	2. commands
	3. command scheduler (like order of code exeuction)
8. logging and telemetry
	1. explain its importance for testing and auditing
	2. realtime vs recorded logging and logging locations
	3. custom logging and automatic logging (wpilib stuff? advantagescope??)
	4. shuffleboard
9. intermediate programming
	1. understanding code execution in detail (like when something gets executed)
	2. how to use abstraction well (in object oriented code, separation of concerns)
	3. intermediate inheritance like subsystem classes and PID subsystem, though most stuff appears to be going towards the functional route??
	4. type casting and null errors
	5. new keyword and pass by value or by reference
	6. function parameters (modifier functions workflow versus member functions)
	7. structured programming https://www.youtube.com/watch?v=7hdJQkn8rtA
10. pneumatic claw subsystem example
	1. include proper waiting for pistons open/close time and also include proper control for solenoids in the open and close command
11. intermediate control systems
	1. PID control
	2. feed forward control https://docs.wpilib.org/en/stable/docs/software/advanced-controls/controllers/feedforward.html
	3. joysticks, controllers, response curves, deadzones, slew rate, and magnitude limits (as a physical property and mechanical property), and units
	4. binding buttons and commands (controls) using wpilib and introduction to triggers
12. flywheel subsystem example
	1. program a flywheel that will use PID and feed forward control loop.
	2. command to set the new velocity control setpoint
13. intermediate units and numbers
	1. coordinate systems for the robot and field
	2. sensor units
	3. importance of standardizing and documenting units
14. elevator subsystem example
	1. program an elevator that uses relative encoders with a limit switch to home.
	2. limit switch wiring to ensure fail safe behavior
	3. command to control the setpoint position (including a manual override option to disable the elevator control loop and to run the motor using a raw input ouput)
15. Swerve drive subsystem
	1. physical setup (measuring the kinematics)
	2. programming of modules and control systems
	3. PID for turning wheels
	4. PID for velocity including feed forward voltage control (including measuring the kinematics of the physical robot)
	5. practical implementation of joystick input. including field oriented drive (with a gyroscope)
	6. swerve path following command
16. advanced programming????????????
	1. https://en.wikipedia.org/wiki/Floating-point_arithmetic (accuracy problems)
	2. how to write good comments
17. 
18. simulation (robot and subsystem)