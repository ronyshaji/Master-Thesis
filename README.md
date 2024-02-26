<h1>Digital Twin: Development and Validation of Vehicle Simulation for Integration of Highly Automated Driving Functions</h1>
<b>Course:</b> <i>International Automotive Engineering, TH Ingolstadt</i></br>
<b>Company:</b> <i>Porsche Engineering Services GmbH, Bietigheim-Bissingen</i></br>
<b>Submitted by:</b> <i>Rony Shaji</i>

![Scenario Based Testing in Virtual Environment](Master Thesis/overview.png)


<h2>Introduction</h2>
Automated and Autonomous driving is currently the most researched topic in the automotive
industry and innovative driver assistance functions are introduced with a focus
on fully autonomous vehicles. Prior to implementing any function in a production vehicle,
safety stands out as a paramount consideration. Ensuring the proper execution of
functions across diverse environmental conditions and scenarios is crucial for maintaining
safety standards. Thorough testing and validation are essential for the functions, encompassing
all conceivable scenarios in which the function must operate, to guarantee flawless
functionality.
</br></br>
Testing functions in real-life situations is nearly impractical due to the multitude of scenarios
involved. This approach demands significant resources, including finances, time,
and manpower, which can substantially impede the progress of autonomous function development.
This is where simulation becomes crucial, offering a means to expedite the
development process efficiently.
</br></br>
The master thesis focuses on the virtual validation of an internal driver assistance function
(Reversing Assist) incorporating scenario-based testing. The Reversing Assist function is
tested using the OpenSCENARIO standard to evaluate the performance and shortcomings
of the functions with respect to different scenarios. The work started with a literature
review of the current state-of-the-art simulation framework to test the driver assistance
functions in the automotive industry. Based on the requirement, the internal simulation
framework is used and the working environment for the simulator is set up.
</br></br>
The Reversing Assist function is built and validated within the simulation framework,
and subsequently, test scenarios are defined to assess its performance. The main use case
of the Reversing Assist function is in the vehicle parking and the scenario is defined on
a parking lot. The scenario is formulated following the OpenSCENARIO standard and
tailored to align with the simulation framework. In the final phase, the function undergoes
testing using the OpenSCENARIO standard, confirming its intended functionality.
During testing, certain limitations in the functions are recognized, paving the way for
potential enhancements.
</br></br>
The <i>Reversing Assist</i> function is available on JUPITER, a ROS-Based Vehicle Platform for
Autonomous Driving Research and the objective of the thesis is to validate the same in a cirtual environment as a part of Digital Twin Implementation. 
</br></br>

 - [JUPITER Source](https://www.ki-deltalearning.de/fileadmin/KI_DeltaLearning/Events/Mid-Term_Presentation/KI_DL_midterm_20211007_Porsche_Engineering_1.pdf)

 - [IEEE Journal](https://ieeexplore.ieee.org/document/9977434)


<h2>Software/Tools</h2>

 - <b><i>Internal Simulation Framework (Improvised CARLA Simulator)
 - ROS Bridge (Windows Subsystem for Linux - WSL)
 - CARLA Scenario Runner
 - Unreal Engine
 - Reverse Assist (ADAS Function)
 - RoadRunner
 - ROS
 - OpenSCENARIO
 - OpenDRIVE
 - Python
 - C++</i></b>

 <h2>Internal Simulation Framework</h2>
It is a virtual testing platform that is developed on top of the automated driving simulator
CARLA 0.9.12 to test and validate driver assistance functions. It has custom sensors
and vehicle models that represent the JUPITER vehicle platform and form the backbone
of digital twin technology. It also can perform scenario-based testing of driving functions
with the use of OpenSCENARIO or CARLA atomic behavior-based testing.
</br></br>
The simulation framework uses a client-server architecture, and the client side consists
of many client modules that control the logic of actors on the simulation server and set
world conditions. Clients communicate with the server using the CARLA Application
Programming Interface (API) in Python/C++, which acts as a communication medium
between the server and clients.</br></br>
The ROS bridge facilitates bidirectional communication between the simulation
server and ROS using the Python/C++ API. This enables the availability of
sensor data on ROS topics, allowing for additional post-processing. Scenario runner allows traffic scenario definition and execution in the simulation server.
In the ROS bridge, the scenario runner is available as a wrapper that enables the execution
of the scenario using the ROS interface. Using this feature, the scenario can be executed
within the ROS bridge and enables communication of other ROS-based functions with
the scenario runner. Reversing Assist is based on the ROS which works by
subscribing and publishing to different ROS topics available in the ROS bridge.</br></br>

 <h2>Working Environment</h2>
The basic working environment for the scenario-based testing can be summarised as follows:

  - <b>Simulation Engine:</b> 
     -    The simulation scene renders the scenes with the meshes and
        provide the environment where the actors can spawn and do actions. Multiple clients can
        communicate with the server at the same time which makes it possible to control different
        parameters at the same time. Different environment conditions like rain, sun, wind, etc
        can be simulated using the server. 
 - <b>Clients:</b>
    - Clients can be communicated with the simualtion engine to perform specific tasks. It tells the simulator to do what task at what time.
 - <b>ROS Bridge:</b>
    - ROS Bridge is a bridge that enables two-way communication between ROS and
the CARLA-based simulation. The information from the simulation server is translated to
various ROS topics which can be used for further processing. The messages sent between
ROS nodes through topics can be sent to the simulation server as a command to perform
various tasks. This feature allows the simulation engine to provide data in the ROS format
which is easy to communicate with other systems. Also, the simulation entities can be
controlled via ROS commands through the ROS bridge.

- <b>Scenario Runner:</b>
    - Scenario runner is based on the CARLA scenario runner which can be used to define
traffic scenarios and execution based on the simulation engine. The scenarios can be
defined in different ways to execute namely based on a Python interface or using open
source standard OpenSCENARIO. Complex traffic scenarios can be tested in different
environmental conditions by creating routes through which the agents can navigate. The
OpenSCENARIO parser takes scenario file and converts to an XML-based file which will
be processed to run the scenarios. The scenario runner can be also executed under the
ROS bridge as a wrapper which improves the useability of the feature.

<h2>ASAM OpenSCENARIO</h2>
OpenSCENARIO defines a file format for the description of dynamic content in driving
simulation applications. It is used to describe complex, synchronized maneuvers that
involve multiple entities like vehicles, pedestrians, and other traffic participants. Different types of scenarios can be defined using the OpenSCENARIO standard and can be used
along with the static road network standard OpenDRIVE.


<h2>Scenario Definition for Reversing Assist Testing</h2>

To validate the Reversing Assist function with OpenSCENARIO, the scenario must be defined first
so that it can be written with OpenSCENARIO syntax. The scenario should include a
forward motion of the vehicle, a standstill condition, and a reverse motion of the vehicle.
The forward motion of the vehicle is controlled by the simulation and the reverse motion is
controlled by the Reversing Assist function. The standstill condition is required so that the vehicle does
not abruptly change direction and acts as a point to start activating the Reversing Assist function.
</br></br>
As the Reversing Assist function is mainly used in the parking lot, the scenario is defined for the
parallel parking of a vehicle starting from the entry of the parking lot. In the figure the dotted line shows the approximate
path the vehicle moves during the forward motion and reverse motion. The yellow and
red line shows the direction of motion of the vehicle during the complete scenario. As
the vehicle uses the custom Simulink physics, the stopping distance can change based
on the velocity condition and the parking position may be changed accordingly. Ideally,
the starting position of the vehicle and the goal position, which is the position where
the vehicle stops after reversing should be the same. But there will be a small tolerance
present because of the stopping distance dependency and Reversing Assist core function.

<h2>Custom Parking lot Map for Evaluation</h2>
Reversing Assist is intended to be used mainly in tightly spaced parking lots where the
vehicle can reverse based on the forward motion. So, to test the Reversing Assist in virtual simulation a
custom parking lot is very much required. RoadRunner, which is owned by MATLAB, is the recommended tool for creating a custom
map because it can export the map in different formats which can be later
imported into the simulation engine. RoadRunner has the option to create different types of roads based on the user’s requirements. 

<h2>OpenSCENARIO Definition for Reversing Assist Testing</h2>

Based on the OpenSCENARIO file, the following three events are created for the scenario based testing. Here the syntax of the OpenSCENARIO standard is used in order to describe the scenario.

 - Event 1 - Forward Motion: Vehicle drives forward using an Autonomous Driving agent
    - MovingForward event is based on RoutingAction.
    - RoutingAction: Specify the route an entity should follow
    - AssignRouteAction – Using waypoints on the road network with the route strategy
    - StartTrigger – MovingForward starts when simulation time starts
    - Simulation controls the forward motion of the vehicle
    
 - Event 2 – Standstill: Vehicle standstill for 1 second after completing the forward motion
    - StandingStill Event with a ‘StandingStill’ Action
    - Longitudinal Action with zero absolute velocity
    - StartTrigger is based on a ConditionGroup in which two conditions are used
    - TriggeringEntities and ReachPositionCondition --> Last waypoint from the Event ‘MovingForward'
 - Event 3 – Reverse Motion: Vehicle follows the forward path and controlled by Reversing Assist
    - Event ‘Reversing Using RA’ comes with a LongitudinalAction 
    - Longitudinal Action with negative absolute velocity --> Target Velocity
    - Negative velocity is required to activate the Reversing Assist within OpenSCENARIO
    - StartTrigger (Event) --> ConditionGroup with TriggeringEntities and StandStillCondition (Based on Event 2) 
    - Reverse motion controlled by the Reversing Assist using Ackermann Control
    - StartTrigger (Act) --> SimulationTimeCondition 
    - StopTrigger (Act) --> ReachPositionCondition --> Initial starting Position
    
<h2>Scenario Evaluation</h2>
    
In the scenario runner, there are atomic evaluation criteria available that analyze
whether the scenario was completed successfully or failed. This is included as a
StopTrigger in the OpenSCENARIO file since there are no evaluation/test criteria available
in the official OpenSCENARIO 1.0 release. To test the Reverse Assist in the OpenSCENARIO, a custom atomic criterion is needed
as the already existing criteria are not suitable to use. The custom atomic criteria or
‘RAScenarioTest’ is used in the OpenSCENARIO file to evaluate the scenario along with
the Reversing Assist. The main idea behind the RAScenarioTest is that it calculates the distance
between the initial starting position of the ego vehicle and the final position of the ego
vehicle after reversing to the starting position. If the distance is less than a threshold value,
the evaluation results will be SUCCESS, meaning the scenario is executed successfully.

<h2>Conclusion</h2>
This thesis emphasized the importance of digital twin and simulation in the testing and validation
of the ADAS function and presented the validation of an internal ADAS function
(Reversing Assist) for automated driving based on OpenSCENARIO incorporating the
ROS framework. For this purpose, the working environment is set up first inside the
Windows OS and Ubuntu inside the WSL. The proper flow of data between the tools/software involved is ensured before testing the ADAS function. A custom ROS node is
created to automate the working and communication of different tools so that the manual
involvement is reduced which in turn speeds up the analysis and validation.
</br></br>
Several OpenSCENARIO files were generated to examine the functionality of OpenSCENARIO
within the scenario runner. Some functions in the file were found to be incompatible
with the existing simulator setup. Through iterative testing, identified issues were
addressed by modifying the OpenSCENARIO to seamlessly integrate with the scenario
runner. The Reversing Assist function is tested using a scenario-based approach utilizing the Open-
SCENARIO to identify the performance and shortcomings of the function. Since the
main use case of the Reversing Assist function is in the parking scenario, a custom parking lot map is
created in MATLAB Roadrunner and later imported into the simulation engine.
</br></br>
The function of the Reversing Assist is to bring back the vehicle to the initial starting position following
the path that the vehicle traveled during the forward motion. The scenario-based testing
evaluation was found to be successful based on the custom criteria, which measures the
difference in the distance between the initial starting position and the final stopping
position. The vehicle was found to be reaching the initial position with a small tolerance
present.</br></br>
One of the main takeaways from this work was the automated testing of the Reversing Assist function
with the OpenSCENARIO. This enables the testing of the Reversing Assist function within the same
scenario, providing a valuable means to compare results after implementing modifications to the function. For instance, there is a need for improvements in the vehicle controller
during reversing, particularly in the vehicle controller. Implementing changes to the vehicle
controller can be efficiently compared through a scenario-based approach, eliminating
the necessity for manual driving to test the vehicle controller modifications.
Though there are some limitations present in the current setup to test the Reversing Assist function
with OpenSCENARIO, this work opens a path for the scenario-based testing of other
ADAS functions using the OpenSCENARIO standard.

