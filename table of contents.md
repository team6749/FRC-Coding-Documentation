- [1. electrical](1.%20electrical.md)
	1. [Motors](1.%20electrical.md#Motors)
	2. [Encoders](1.%20electrical.md#Encoders)
	3. [Pneumatics](1.%20electrical.md#Pneumatics)
	4. [Switch](1.%20electrical.md#Switch)
	5. [Accelerometers](1.%20electrical.md#MEMS%20Gryoscopes%20and%20Accelerometers)
	6. [Sensors](1.%20electrical.md#misc%20sensors)
- [2. computers and programs](2.%20computers%20and%20programs.md)
	1. [Data Storage](2.%20computers%20and%20programs.md#binary%20and%20data%20storage)
	2. [Boolean Algebra](2.%20computers%20and%20programs.md#intro%20logic%20and%20boolean%20algebra)
	3. [BASIC](2.%20computers%20and%20programs.md#BASIC%20programming%20(literally))
	4. [How Computers Think](2.%20computers%20and%20programs.md#how%20computers%20think)
- [3. software collaboration](3.%20software%20collaboration.md)
	1. [Git](3.%20software%20collaboration.md#git)
	3. [Workflow Dependencies](3.%20software%20collaboration.md#workflow%20dependencies)
	4. [Hardware](3.%20software%20collaboration.md#hardware)
	5. [Testing](3.%20software%20collaboration.md#testing)
- [4. intro control systems](4.%20intro%20control%20systems.md)
	1. [Closed Loop](4.%20intro%20control%20systems.md#open%20loop%20vs%20closed%20loop)
	3. how we might want to go about controlling a motor using pseudocode. explain concepts like how a loop works (program a thermostat in this example using the sensor to explain how timing works and relate specifically to robot code timings like the periodic loops)
- [5. basic programming](5.%20basic%20programming.md)
	1. [Make a Website](5.%20basic%20programming.md#make%20a%20website)
	2. [Intro to Java](5.%20basic%20programming.md#intro%20to%20java)
- [6. loop based programming](6.%20loop%20based%20programming.md)
- [7. command based programming](7.%20command%20based%20programming.md)
	1. [Subsystems](7.%20command%20based%20programming.md#Subsystem)
		- when to and when to not use a subsystem in general (and which implementation to use)
	2. [Command](7.%20command%20based%20programming.md#Command)
	3. [Scheduler](7.%20command%20based%20programming.md#Scheduler)
	4. [Command Based Robots](7.%20command%20based%20programming.md#Programming%20Command%20Based%20Robots)
- [8. logging and telemetry](8.%20logging%20and%20telemetry.md)
	1. [Programming](8.%20logging%20and%20telemetry.md#programming)
- [9. intermediate programming](9.%20intermediate%20programming.md)
	1. understanding code execution in detail (call stack on scheduler)
- [10. intermediate control systems](10.%20intermediate%20control%20systems.md)
	1. PID implementation and potential issues
	2. feed forward control https://docs.wpilib.org/en/stable/docs/software/advanced-controls/controllers/feedforward.html
	3. joysticks, controllers, response curves, deadzones, slew rate, and magnitude limits (as a physical property and mechanical property), and units
	4. binding buttons and commands (controls) using wpilib and introduction to triggers
	5. explain debouncing and basics of digital signal processing with examples of noisy sensor data.
- flywheel subsystem example
	1. program a flywheel that will use PID and feed forward control loop.
	2. command to set the new velocity control setpoint
- [12. pneumatic claw subsystem](12.%20pneumatic%20claw%20subsystem.md)
	1. include proper waiting for pistons open/close time and also include proper control for solenoids in the open and close command
- units and numbers
	1. coordinate systems for the robot and field
	2. sensor units
	3. importance of standardizing and documenting units
	4. [](resources.md#Math)
- elevator subsystem example
	1. program an elevator that uses relative encoders with a limit switch to home.
	2. limit switch wiring to ensure fail safe behavior
	3. command to control the setpoint position (including a manual override option to disable the elevator control loop and to run the motor using a raw input ouput)
- Swerve drive subsystem
	1. physical setup (measuring the kinematics)
	2. programming of modules and control systems
	3. PID for turning wheels
	4. PID for velocity including feed forward voltage control (including measuring the kinematics of the physical robot)
	5. practical implementation of joystick input. including field oriented drive (with a gyroscope)
	6. swerve path following command
- redundancy and safety 
	- **handling hardware failures**
	- controls overrides (differing levels of control for subsystems)
	- each subsystem should have control at all levels of automation. This means even if the part is controlled using PID (like a robot arm segment), it should still have a method of manual control for debugging and reliability.
- vision and robot positioning
	- global vs local state
	- practical uses for computer vision in FRC
	- sensor fusion
- robot simulation (including individual subsystem simulation)
- unit testing