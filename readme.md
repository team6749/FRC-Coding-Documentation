
There will be a set learning path along with links everywhere. Please read these links as they are part of the content of the course. #todo I will emphasise important links and "just for reference" links separately. The goal is to get someone with almost no knowledge able to feel comfortable with the concepts of programming a robot at their own pace. This guide is NOT exaustive, but attempts to be extensive without too much overlap or jumping.



---

# outline
- how to program robots and best practices surrounding it
	- command based programming
		- subsystems
			- what is a subsystem (it describes the physicality of the robot and it controls that part)
			- [[PID]] only subsystems
			- when to and when to not use a subsystem in general (and which implementation to use)
		- commands
			- what is a command
			- how do commands relate to subsystems
		- command scheduler
	- logging and telemetry
		- logging locations (on robot versus on driver station and the implications)
		- logging tools like shuffleboard
		- phoenix tuner can be used to graph and tune [[PID]] values easily by graphing the systems control loop. (alternatively this can be done with shuffleboard???????????)
	- safety features and redundancy
		- handling hardware failures
		- controls overrides (differing levels of control for subsystems)
			- each subsystem should have control at all levels of automation. This means even if the part is controlled using PID (like a robot arm segment), it should still have a method of manual control
- systems design
	- https://en.wikipedia.org/wiki/Control_system
		- open and closed loop
	- 
- Specific implementations and guidelines
	- [[PID]]
	- wrapping values from sensors (modulo math)
	- How to pick units and related things (also modulo math (: )
	- vision
		- global vs local state
		- sensor fusion
	- binding buttons and commands (controls)
	- 
- index of resources
	- wpilib
	- programming tutorials?
	- previous season examples (dont actually put it in here though put it where relevant)
- software plus hardware
	- workflows for software development and how to integrate it into the hardware lifecycle
		- git workflow
		- how to **prioritize** and create issues
			- typical hardware year will start with prototyping and testing (software should work with electrical hardware to have development platforms ready to test)
			- a good way to test mechanisms might be a previous year robot hardware and code