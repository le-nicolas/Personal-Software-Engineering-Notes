The most common frameworks for robot software development. It provides standard formats for robot descriptions, messages, and data types for use cases as varied as industrial assembly, autonomous vehicles and entertainment. 

This is a vibrant user community contributes many open source packages for common functionalities that can bootstrap the development of new systems.

Roboticists often architect a robot application as a modular set of ROS nodes that can be deployed both to real robots and to computers that interface with simulators. In a simulation, developers build a virtual world that mirrors the real robot’s target use case. By testing in this simulated ecosystem, users can iterate on designs quickly before testing in the real world and ultimately deploying to production.



A great example is a simple pick and place manipulation task. 

	1. Defining the robot's task
	The six-axis Niryo One serves as the robot arm. The environment is minimal: an empty room, a table on which the robot sits, and a cube(i.e., the target object). To accomplish the motion-planning ROS packages colelctively we use MoveIt. When we are ready to start the task, we send a planning request from the simulator to MoveIt. The request contains the poses of all the robot's joints, the cube's pose, and the target position of the cube. MoveIt then computes a motion plan and sends this plan back to the simulator for execution. 
	
	2. Use Unity and connect it to ROS
	Now that the robot is in the Unity editor, we should test our motion-planning algorithm, running in a set  of ROS nodes. Set up a comms interface between Unity and ROS. Unity needs to pass messages to ROS that contain state information - the poses of the robot, target object, and target location - along with a planning request to the mover service. In turn, ROS needs to return a trajectory message to Unity corresponding to the motion plan ( in other words, the sequence of joint positions required to complete the pick-and-place task).
	
Since communication in ROS uses a pub/sub model, the first requirement for ROS-Unity communication is classes in Unity corresponding to ROS message types. 
	When user add the ROS-TCP-Connector Unity package to the Unity Editor, users can use the MessageGeneration plugin to generate C# classes, including serialization and deserialization functions, from ROS .msg and .srv files. 
	
Note that the ROS-TCP-Connector package also includes scripts that the user can extend to publish messages from Unity to a ROS topic, subscribe in Unity to Messages on a ROS topic, and create ROS service requests and responses. On the ROS side, a ROS package called ROS-TCP-Endpoint can create an endpoint to enable communication between ROS nodes  and a Unity Scene using these ROS-TCP-Connector scripts.

To use these
	Ø Use the ROS-Unity integration packages to create a publisher in Unity to send the pose data to ROS over TCP. On the ROS side, we need to set up a ROS-TCP-Endpoint to subscribe to these pose messages.
	Ø Create a "Publish" button in the Unity Scene along with an OnClick callback. This callback function makes a service request to the MoveIt motion planner. The service request includes the current pose of the robot, the pose of the target object, and the target location. When MoveIt receives the planning request, it attempts to compute a motion plan. If successful, the service returns the plan, i.e. a sequence of joint positions, and a Unity script executes the trajectory using the ArticulationBody APIs. Otherwise, it returns a failure message.

Unity and autonomy - study and developemnt of algorithms capable of making decision in the absence of strict rules defined by a human developer, and simulation supports this transition by enabling greater flexibility and faster experimentation than real-world testing. 

Simulation powering autonomy
	- Autonomy again means the decisions of a robot makes and the results of those decisions are not neatly predictable using only a state machine and a collection of mathematical formulae.
	- If a robot is expected to sense an environment, a simulation must be capable of accurately modeling those sensors without making compromises with respect to the accuracy of the environment's simulated topology and physics. 
		○ If there are other agents in that environment (people or other robots) then the simulation must be capable of modeling the agent behavior, while still maintaining the accuracy of its sensor simulation, topology representation, and physics modeling.
		○ Thus, we need four things: flexibility, extensibility, scalability and fidelity.

Another sample of a digital twin




Recreated the Unity Brighton office
	Thru a web interface, you can check maintenance systems, check out camera feeds, and get updates on any security events.
	

Another example



The metadata component was created for each imported building part by the Pixyz plugin when the model was imported from Revit. This is an example of one of the numerous ways the Unity Editor can access data to create digital twins. 

From <https://learn.unity.com/tutorial/introduction-to-digital-twins-with-unity#660c74d7edbc2a229ece6a17> 


This script iterates through all the objects in the building model and uses the metadata to find the floor objects. Once a floor is detected, it adds a navmesh component and then bakes the scene navmesh.

From <https://learn.unity.com/tutorial/introduction-to-digital-twins-with-unity#> 



