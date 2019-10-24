<!--- This file is generated from the SmartCdlServer.componentDocumentation model --->
<!--- do not modify this file manually as it will by automatically overwritten by the code generator, modify the model instead and re-generate this file --->

# SmartCdlServer Component

<img src="model/SmartCdlServerComponentDefinition.jpg" alt="SmartCdlServer-ComponentImage" width="1000">

<p>The SmartCdlServer is based on the <b>Curvature Distance Lookup (CDL)</b> algorithm for fast local obstacle avoidance.
</p>
<p> The CDL algorithm is an improvement of the dynamic window approach. It considers the dynamics and kinematics of the robot,
 as well as its polygonal shape. It consumes raw laser scans or other sensor perceptions transformed into occupancy grids.
 The basic idea is that a robot moves along different curvatures (v, w combinations) which represent trajectories built up
 by circular arcs. The huge number of possible v, w combinations is reduced based on the observation that only a few curvatures are
 safely selectable given the current state and kinematics of the robot. Curvatures leading to a collision are discarded.
 High performance advantages are achieved by precalculating lookup tables. The final selection along the remaining admissible v, w combinations
 is done by an objective function, which trades off speed, goal-directedness and remaining distance until collision.
</p>
<p> This objective function together with its weighting factors build different strategies, such as reactive driving,
 joystick navigation, rotating or approaching goals. The strategies are used for the selection of the best-fitting curvature with
 respect to the purpose of the strategy. Example strategies are passing over intermediate waypoints, approaching a goal given by a
 path-planner or following a person.
</p>
<p> The SmartCdlServer will read files which contain precalculated lookup tables generated by <b>smartCdlCalculate</b> utility (see SmartSoft UtilityRepository).
 They contain the kinematics of the robot.
</p>
<p> SmartCdlServer supports differential drive, synchro drive and omnidrive if neglecting lateral velocity.
</p>
<p> Note: This component is used in Tutorials (e.g. <i>Lesson 1</i>).
</p>
<p> See also:
 Christian Schlegel. Fast local obstacle avoidance under kinematic and dynamic constraints for a mobile robot.
 In Proc. Int. Conf. on Intelligent Robots and Systems (IROS), p. 594-599, Victoria, Canada, 1998.
</p>
<p></p>

## Component-Datasheet Properties

<table style="border-collapse:collapse;">
<caption>Component-Datasheet Properties</caption>
<tr style="background-color:#ccc;">
<th style="border:1px solid black; padding: 5px;"><i>Property Name</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Property Value</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Property Description</i></th>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;">SpdxLicense</td>
<td style="border:1px solid black; padding: 5px;">LGPL-2.0-or-later</td>
<td style="border:1px solid black; padding: 5px;">https://spdx.org/licenses/LGPL-2.0-or-later.html</td>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;">TechnologyReadinessLevel</td>
<td style="border:1px solid black; padding: 5px;">TRL5</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;">Homepage</td>
<td style="border:1px solid black; padding: 5px;">http://servicerobotik-ulm.de/components</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;">Supplier</td>
<td style="border:1px solid black; padding: 5px;">Servicerobotics Ulm</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;">Purpose</td>
<td style="border:1px solid black; padding: 5px;">Navigation</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;">Memory</td>
<td style="border:1px solid black; padding: 5px;">20000 KB</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;">Capability</td>
<td style="border:1px solid black; padding: 5px;">CollisionAvoidance</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
</table>

## Component Ports

### LaserClient

 Incoming laser scans that the CDL algorithm uses for obstacle avoidance, e.g. from SmartLaserLMS200Server

<table style="border-collapse:collapse;">
<caption>Component-Port Datasheet Properties of <b>LaserClient</b></caption>
<tr style="background-color:#ccc;">
<th style="border:1px solid black; padding: 5px;"><i>Property Name</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Property Value</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Property Description</i></th>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;">CoordnateDimensions</td>
<td style="border:1px solid black; padding: 5px;">2D</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
</table>


### LaserClient2

 Second (optional) laser client allows using two laser-scanners concurrently


### PlannerClient

 Goals from planner (e.g. smartPlannerBreathFirstSearch) can be sent to this port


### NavVelSendServer

<p>Navigation commands <b>v</b> and <b>w</b> sent via this port will be considered when chosing a trajectory.
</p>
<p> This port can be used to ensure collision free navigation while following incoming navigation commands
 from e.g. a joystick (e.g. SmartExampleJoystickNavigationClient) as close as possible.
 This port accepts inputs only if strategy JOYSTICK is set.
</p>
<p> See strategy JOYSTICK.
</p>
<p></p>

<table style="border-collapse:collapse;">
<caption>Component-Port Datasheet Properties of <b>NavVelSendServer</b></caption>
<tr style="background-color:#ccc;">
<th style="border:1px solid black; padding: 5px;"><i>Property Name</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Property Value</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Property Description</i></th>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;">CoordnateDimensions</td>
<td style="border:1px solid black; padding: 5px;">2D</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
</table>


### TrackingClient

 Goals from tracking can be sent to this port. (e.g. smartLaserPersonTracker)


### IRClient



### PathNavigationGoalClient



### BaseStateClient


<table style="border-collapse:collapse;">
<caption>Component-Port Datasheet Properties of <b>BaseStateClient</b></caption>
<tr style="background-color:#ccc;">
<th style="border:1px solid black; padding: 5px;"><i>Property Name</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Property Value</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Property Description</i></th>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;">CoordnateDimensions</td>
<td style="border:1px solid black; padding: 5px;">2D</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
</table>


### NavVelSendClient

 Typically connected to the robot base (e.g. SmartPioneerBaseServer). This port sends navigation commands v, w.

<table style="border-collapse:collapse;">
<caption>Component-Port Datasheet Properties of <b>NavVelSendClient</b></caption>
<tr style="background-color:#ccc;">
<th style="border:1px solid black; padding: 5px;"><i>Property Name</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Property Value</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Property Description</i></th>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;">MotionPrimitive</td>
<td style="border:1px solid black; padding: 5px;">DifferentialDrive</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;">CoordnateDimensions</td>
<td style="border:1px solid black; padding: 5px;">2D</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
</table>


### GoalEventServer

<p>Register with event state CDL_GOAL_NOT_REACHED to be notified when the stateful event switches to event state CDL_GOAL_REACHED.
</p>
<p> The CDL_GOAL_REACHED will be sent only once per activation.
 CDL_GOAL_REACHED event is sent when a goal was reached (i.e. the robot is within goal distance or angle error).
</p>
<p> ComponentMode Neutral : Port is neutral, does not consume new input while in this state.
 ComponentMode MoveRobot : Will send goal reached events.
</p>
<p></p>


### RobotBlockedEventServer





## Component Parameters: SmartCdlServerParams

### Internal Parameter: PathNav


<table style="border-collapse:collapse;">
<caption>Internal Parameter: <b>PathNav</b></caption>
<tr style="background-color:#ccc;">
<th style="border:1px solid black; padding: 5px;"><i>Attribute Name</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Attribute Type</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Attribute Value</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Attribute Description</i></th>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>pathNavPredictedGoalPose_controll1_dist</b></td>
<td style="border:1px solid black; padding: 5px;">Double</td>
<td style="border:1px solid black; padding: 5px;">200.0</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>pathNavPredictedGoalPose_controll1_speed</b></td>
<td style="border:1px solid black; padding: 5px;">Double</td>
<td style="border:1px solid black; padding: 5px;">100.0</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>pathNavPredictedGoalPose_controll2_dist</b></td>
<td style="border:1px solid black; padding: 5px;">Double</td>
<td style="border:1px solid black; padding: 5px;">300.0</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>pathNavPredictedGoalPose_controll2_speed</b></td>
<td style="border:1px solid black; padding: 5px;">Double</td>
<td style="border:1px solid black; padding: 5px;">250.0</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>pathNavPredictedGoalPose_controll3_dist</b></td>
<td style="border:1px solid black; padding: 5px;">Double</td>
<td style="border:1px solid black; padding: 5px;">600.0</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>pathNavPredictedGoalPose_controll3_speed</b></td>
<td style="border:1px solid black; padding: 5px;">Double</td>
<td style="border:1px solid black; padding: 5px;">600.0</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>pathNavPredictedGoalPose_minDist</b></td>
<td style="border:1px solid black; padding: 5px;">Double</td>
<td style="border:1px solid black; padding: 5px;">200</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>pathNavRecover_max_dist</b></td>
<td style="border:1px solid black; padding: 5px;">Double</td>
<td style="border:1px solid black; padding: 5px;">2000</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>robotBlocked_event_timeout</b></td>
<td style="border:1px solid black; padding: 5px;">UInt16</td>
<td style="border:1px solid black; padding: 5px;">15</td>
<td style="border:1px solid black; padding: 5px;"><p>timout for robot beeing block in secons
</p></td>
</tr>
</table>

### Internal Parameter: Cdl


<table style="border-collapse:collapse;">
<caption>Internal Parameter: <b>Cdl</b></caption>
<tr style="background-color:#ccc;">
<th style="border:1px solid black; padding: 5px;"><i>Attribute Name</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Attribute Type</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Attribute Value</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Attribute Description</i></th>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>dataDir</b></td>
<td style="border:1px solid black; padding: 5px;">String</td>
<td style="border:1px solid black; padding: 5px;">"data/lookup-files/"</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>curvature_default_file</b></td>
<td style="border:1px solid black; padding: 5px;">String</td>
<td style="border:1px solid black; padding: 5px;">"CDLindex_P3DX.dat"</td>
<td style="border:1px solid black; padding: 5px;"><p>File with the curvature indices as produced by cdlCalculate. Relative to current dir or absolute. See also parameter LOOKUPTABLE().
</p></td>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>lookup_default_file</b></td>
<td style="border:1px solid black; padding: 5px;">String</td>
<td style="border:1px solid black; padding: 5px;">"CDLdist_P3DX.dat"</td>
<td style="border:1px solid black; padding: 5px;"><p>File with the distance values as produced by cdlCalculate. Relative to current dir or absolute. See also parameter LOOKUPTABLE().
</p></td>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>lookup_default_file_compressed</b></td>
<td style="border:1px solid black; padding: 5px;">Boolean</td>
<td style="border:1px solid black; padding: 5px;">false</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>accel_default_file</b></td>
<td style="border:1px solid black; padding: 5px;">String</td>
<td style="border:1px solid black; padding: 5px;">"CDLacc_P3DX.dat"</td>
<td style="border:1px solid black; padding: 5px;"><p>File with the allowed accelerations as produced by cdlCalculate. Relative to current dir or absolute. See also parameter LOOKUPTABLE().
</p></td>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>curvature_second_file</b></td>
<td style="border:1px solid black; padding: 5px;">String</td>
<td style="border:1px solid black; padding: 5px;">"CDLindex_P3DX.dat"</td>
<td style="border:1px solid black; padding: 5px;"><p>File with the curvature indices as produced by cdlCalculate. Relative to current dir or absolute. See also parameter LOOKUPTABLE().
</p></td>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>lookup_second_file</b></td>
<td style="border:1px solid black; padding: 5px;">String</td>
<td style="border:1px solid black; padding: 5px;">"CDLdist_P3DX.dat"</td>
<td style="border:1px solid black; padding: 5px;"><p>File with the distance values as produced by cdlCalculate. Relative to current dir or absolute. See also parameter LOOKUPTABLE().
</p></td>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>lookup_second_file_compressed</b></td>
<td style="border:1px solid black; padding: 5px;">Boolean</td>
<td style="border:1px solid black; padding: 5px;">false</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>accel_second_file</b></td>
<td style="border:1px solid black; padding: 5px;">String</td>
<td style="border:1px solid black; padding: 5px;">"CDLacc_P3DX.dat"</td>
<td style="border:1px solid black; padding: 5px;"><p>File with the allowed accelerations as produced by cdlCalculate. Relative to current dir or absolute. See also parameter LOOKUPTABLE().
</p></td>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>translation_acc</b></td>
<td style="border:1px solid black; padding: 5px;">Double</td>
<td style="border:1px solid black; padding: 5px;">400.0</td>
<td style="border:1px solid black; padding: 5px;"><p>Translational acceleration. [mm/s^2]
</p></td>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>rotation_acc</b></td>
<td style="border:1px solid black; padding: 5px;">Double</td>
<td style="border:1px solid black; padding: 5px;">100.0</td>
<td style="border:1px solid black; padding: 5px;"><p>Rotational acceleration. [deg/s^2]
</p></td>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>delta_t_calc</b></td>
<td style="border:1px solid black; padding: 5px;">Double</td>
<td style="border:1px solid black; padding: 5px;">0.35</td>
<td style="border:1px solid black; padding: 5px;"><p>CDL predicts the robot motion deltacalc timesteps into the future. (10Hz was 0.7 now with 20Hz 0.35 Matthias)
</p></td>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>delta_t_trigger</b></td>
<td style="border:1px solid black; padding: 5px;">Double</td>
<td style="border:1px solid black; padding: 5px;">0.1</td>
<td style="border:1px solid black; padding: 5px;"><p>The time steps for the CDL execution cycle. Defines the rate in which the CDL task is executed.
</p></td>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>followHysteresis</b></td>
<td style="border:1px solid black; padding: 5px;">Boolean</td>
<td style="border:1px solid black; padding: 5px;">false</td>
<td style="border:1px solid black; padding: 5px;"><p>In following mode: if true, the robot will only follow the person if the person moved a considerably distance.
</p></td>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>contour_default_file</b></td>
<td style="border:1px solid black; padding: 5px;">String</td>
<td style="border:1px solid black; padding: 5px;">"CDLcontour_P3DX.dat"</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>contour_second_file</b></td>
<td style="border:1px solid black; padding: 5px;">String</td>
<td style="border:1px solid black; padding: 5px;">"CDLcontour_P3DX.dat"</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>use_obstacle_history</b></td>
<td style="border:1px solid black; padding: 5px;">Boolean</td>
<td style="border:1px solid black; padding: 5px;">false</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>freeBehaviorDist</b></td>
<td style="border:1px solid black; padding: 5px;">Double</td>
<td style="border:1px solid black; padding: 5px;">350.0</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>freeBehaviorDist_second</b></td>
<td style="border:1px solid black; padding: 5px;">Double</td>
<td style="border:1px solid black; padding: 5px;">350.0</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
</table>

### Internal Parameter: CdlRotate


<table style="border-collapse:collapse;">
<caption>Internal Parameter: <b>CdlRotate</b></caption>
<tr style="background-color:#ccc;">
<th style="border:1px solid black; padding: 5px;"><i>Attribute Name</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Attribute Type</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Attribute Value</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Attribute Description</i></th>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>error</b></td>
<td style="border:1px solid black; padding: 5px;">Double</td>
<td style="border:1px solid black; padding: 5px;">5.0</td>
<td style="border:1px solid black; padding: 5px;"><p>Define allowed error for in place rotation [deg]. Similar to goalregion for rotation.
</p></td>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>rotDev1</b></td>
<td style="border:1px solid black; padding: 5px;">Double</td>
<td style="border:1px solid black; padding: 5px;">1.0</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>rotDev2</b></td>
<td style="border:1px solid black; padding: 5px;">Double</td>
<td style="border:1px solid black; padding: 5px;">1.0</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>rotDev3</b></td>
<td style="border:1px solid black; padding: 5px;">Double</td>
<td style="border:1px solid black; padding: 5px;">15.0</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>rotDev4</b></td>
<td style="border:1px solid black; padding: 5px;">Double</td>
<td style="border:1px solid black; padding: 5px;">45.0</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>rotSpeed1</b></td>
<td style="border:1px solid black; padding: 5px;">Double</td>
<td style="border:1px solid black; padding: 5px;">0.0</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>rotSpeed2</b></td>
<td style="border:1px solid black; padding: 5px;">Double</td>
<td style="border:1px solid black; padding: 5px;">2.0</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>rotSpeed3</b></td>
<td style="border:1px solid black; padding: 5px;">Double</td>
<td style="border:1px solid black; padding: 5px;">10.0</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>rotSpeed4</b></td>
<td style="border:1px solid black; padding: 5px;">Double</td>
<td style="border:1px solid black; padding: 5px;">70.0</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
</table>

### Internal Parameter: Server


<table style="border-collapse:collapse;">
<caption>Internal Parameter: <b>Server</b></caption>
<tr style="background-color:#ccc;">
<th style="border:1px solid black; padding: 5px;"><i>Attribute Name</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Attribute Type</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Attribute Value</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Attribute Description</i></th>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>plannerInit</b></td>
<td style="border:1px solid black; padding: 5px;">Boolean</td>
<td style="border:1px solid black; padding: 5px;">true</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>trackerInit</b></td>
<td style="border:1px solid black; padding: 5px;">Boolean</td>
<td style="border:1px solid black; padding: 5px;">false</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>laserClient2Init</b></td>
<td style="border:1px solid black; padding: 5px;">Boolean</td>
<td style="border:1px solid black; padding: 5px;">false</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>irClientInit</b></td>
<td style="border:1px solid black; padding: 5px;">Boolean</td>
<td style="border:1px solid black; padding: 5px;">false</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>pathNavInit</b></td>
<td style="border:1px solid black; padding: 5px;">Boolean</td>
<td style="border:1px solid black; padding: 5px;">false</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>baseClientInit</b></td>
<td style="border:1px solid black; padding: 5px;">Boolean</td>
<td style="border:1px solid black; padding: 5px;">false</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
</table>

### ParameterSetInstance: CdlParameter

#### Trigger Instance: SETSTRATEGY

is-active: <b>false</b>

<p>Set the CDL strategy. Available strategies:
</p>
<p>- REACTIVE: Reactive driving. The robot tries to maximize its speed by avoiding any obstacles. It will drive into the direction which allows the highest translational velocity and provides the largest remaining travel distance. This is the default value.
- JOYSTICK: The robot can be controlled with a joystick. The CDL takes input from the port navigationVelocitySendServer and choses a trajectory closest to the v, w commands given by the joystick. See also server port navigationVelocitySendServer.
- APPROACH_HALT: Approach a goal and halt when reached. Will send a CDL_GOAL_REACHED event via the cdlGoalEventServer when the goal is reached. Possible goal modes: ABSOLUTE, PLANNER.
- APPROACH: Approach a target but switch to REACTIVE when the goal is reached rather than stopping as in strategy APPROACH_HALT. Will send a CDL_GOAL_REACHED event via the cdlGoalEventServer when the goal is reached. Can be used to achieve smooth movement when using intermediate goal points. Goal modes: ABSOLUTE, PLANNER.
- ROTATE: Rotate into the given direction and report this by the CDL_GOAL_REACHED event. The heading can be given by absolute position, absolute angle or relative angle. Goal modes: ABSOLUTE, ANGLEABSOLUTE, ANGLERELATIVE.
- FOLLOW: Drive into the given direction with the given translational velocity. Takes goals from the trackingClient port. Used e.g. by the smartLaserPersonTracker. Goal modes: PERSON.
- BACKWARD: Move blindly backwards and stop as soon as the given distance has been covered. The distance is calculated to a previously saved position (parameter SAVECURPOS()). Note that this is blind driving. This strategy can be used if a mobile platform has no laser scanner mounted that points backwards. Fires CDL_GOAL_REACHED when distance has been covered.
- PATH_NAV: TODO
</p>
<p></p>
<p></p>

#### Parameter Instance: FREEBEHAVIOR

<p>Activate or deactivate the free behavior in stalled situations. If activated, the robot will turn in a free direction in stalled situations. Values: ACTIVATE, DEACTIVATE
</p>

<table style="border-collapse:collapse;">
<caption>Parameter-Instance: <b>FREEBEHAVIOR</b></caption>
<tr style="background-color:#ccc;">
<th style="border:1px solid black; padding: 5px;"><i>Attribute Name</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Attribute Type</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Attribute Value</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Attribute Description</i></th>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>free</b></td>
<td style="border:1px solid black; padding: 5px;">InlineEnumeration</td>
<td style="border:1px solid black; padding: 5px;">DEACTIVATE</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
</table>

#### Parameter Instance: PATHNAVFREEBEHAVIOR


<table style="border-collapse:collapse;">
<caption>Parameter-Instance: <b>PATHNAVFREEBEHAVIOR</b></caption>
<tr style="background-color:#ccc;">
<th style="border:1px solid black; padding: 5px;"><i>Attribute Name</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Attribute Type</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Attribute Value</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Attribute Description</i></th>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>free</b></td>
<td style="border:1px solid black; padding: 5px;">InlineEnumeration</td>
<td style="border:1px solid black; padding: 5px;">DEACTIVATE</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
</table>

#### Parameter Instance: LOOKUPTABLE

<p>Changes the lookup table. Lookup tables are precalculated in files and contain the kinematics and shape of the robot. Two lookup files can be specified in the ini configuration. This parameter allows to switch between these lookup tables at runtime. Note that you can use this parameter only in state neutral. Values: DEFAULT, SECOND. See Ini-Configuration.
</p>

<table style="border-collapse:collapse;">
<caption>Parameter-Instance: <b>LOOKUPTABLE</b></caption>
<tr style="background-color:#ccc;">
<th style="border:1px solid black; padding: 5px;"><i>Attribute Name</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Attribute Type</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Attribute Value</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Attribute Description</i></th>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>lt</b></td>
<td style="border:1px solid black; padding: 5px;">InlineEnumeration</td>
<td style="border:1px solid black; padding: 5px;">DEFAULT</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
</table>

#### Parameter Instance: TRANSVEL

<p>Set translation velocity ?vmin, ?vmax in [mm/s]. The values are thresholded by the robot's vmin and vmax inputs to calculate the lookup tables in cdlCalculate (CDL_V_TRA_).
</p>

<table style="border-collapse:collapse;">
<caption>Parameter-Instance: <b>TRANSVEL</b></caption>
<tr style="background-color:#ccc;">
<th style="border:1px solid black; padding: 5px;"><i>Attribute Name</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Attribute Type</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Attribute Value</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Attribute Description</i></th>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>vmin</b></td>
<td style="border:1px solid black; padding: 5px;">Double</td>
<td style="border:1px solid black; padding: 5px;">0.0</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>vmax</b></td>
<td style="border:1px solid black; padding: 5px;">Double</td>
<td style="border:1px solid black; padding: 5px;">400.0</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
</table>

#### Parameter Instance: ROTVEL

<p>Set rotation velocity minimum/maximum values ?wmin, ?wmax in [deg/s]. The values are thresholded by the robot's wmin and wmax inputs to calculate the lookup tables in cdlCalculate (CDL_V_ROT_).
</p>

<table style="border-collapse:collapse;">
<caption>Parameter-Instance: <b>ROTVEL</b></caption>
<tr style="background-color:#ccc;">
<th style="border:1px solid black; padding: 5px;"><i>Attribute Name</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Attribute Type</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Attribute Value</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Attribute Description</i></th>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>wmin</b></td>
<td style="border:1px solid black; padding: 5px;">Double</td>
<td style="border:1px solid black; padding: 5px;">-40.0</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>wmax</b></td>
<td style="border:1px solid black; padding: 5px;">Double</td>
<td style="border:1px solid black; padding: 5px;">40.0</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
</table>

#### Parameter Instance: GOALMODE

<p>Set goal type and goal source. Available modes:
</p>
<p>- ABSOLUTE: Use absolute goal position. Can only be used for goals that do not require path planning, as the CDL cannot handle local minimas. See strategies. Goal can be set with parameter GOALREGION(?x)(?y)(?a)(?id), while ?a is ignored. Used to approach a goal exactly.
- PLANNER: Goal specification from planner, port plannerClient. Typically used with path planners (e.g. smartPlannerBreathFirstSearch).
- PERSON: Optimized parameters for person approaching, port trackingClient (e.g. smartLaserPersonTracker).
- SAVED: Used for backward driving (strategy BACKWARD) as a point of reference to calculate the driven distance. The reference point must be saved with SAVECURPOS() first.
- ANGLEABSOLUTE: Heading is given by an absolute angle [deg]. Used with strategy ROTATE as a reference. Goal direction first must be set with parameter GOALREGION(?x)(?y)(?a)(?id) while ?x and ?y are ignored.
- ANGLERELATIVE: Heading is given by an angle [deg] relative to robot. Used with strategy ROTATE as a reference. Goal direction must be set with parameter GOALREGION(?x)(?y)(?a)(?id) while ?x and ?y are ignored. Rotates then relative to this saved position.
- PATH_NAV: TODO
</p>
<p></p>
<p></p>

<table style="border-collapse:collapse;">
<caption>Parameter-Instance: <b>GOALMODE</b></caption>
<tr style="background-color:#ccc;">
<th style="border:1px solid black; padding: 5px;"><i>Attribute Name</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Attribute Type</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Attribute Value</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Attribute Description</i></th>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>gm</b></td>
<td style="border:1px solid black; padding: 5px;">InlineEnumeration</td>
<td style="border:1px solid black; padding: 5px;">NEUTRAL</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
</table>

#### Parameter Instance: GOALREGION

<p>Set goal: ?x, ?y, angle ?a, id ?id. Sends an event CDL_GOAL_NOT_REACHED once a new goal is set. CDL_GOAL_REACHED is sent as soon as the goal is reached. All values must be set while ?x/?y or ?a may be ignored depending on the strategy and goalmode.
</p>

<table style="border-collapse:collapse;">
<caption>Parameter-Instance: <b>GOALREGION</b></caption>
<tr style="background-color:#ccc;">
<th style="border:1px solid black; padding: 5px;"><i>Attribute Name</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Attribute Type</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Attribute Value</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Attribute Description</i></th>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>goalX</b></td>
<td style="border:1px solid black; padding: 5px;">Double</td>
<td style="border:1px solid black; padding: 5px;">0.0</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>goalY</b></td>
<td style="border:1px solid black; padding: 5px;">Double</td>
<td style="border:1px solid black; padding: 5px;">0.0</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>goalA</b></td>
<td style="border:1px solid black; padding: 5px;">Double</td>
<td style="border:1px solid black; padding: 5px;">0.0</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
</table>

#### Trigger Instance: SETGOALREGION

is-active: <b>false</b>


#### Parameter Instance: APPROACHDIST

<p>Set goal approach distance [mm]. The robot will approach until goal is within this distance.
</p>

<table style="border-collapse:collapse;">
<caption>Parameter-Instance: <b>APPROACHDIST</b></caption>
<tr style="background-color:#ccc;">
<th style="border:1px solid black; padding: 5px;"><i>Attribute Name</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Attribute Type</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Attribute Value</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Attribute Description</i></th>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>approachDistance</b></td>
<td style="border:1px solid black; padding: 5px;">Double</td>
<td style="border:1px solid black; padding: 5px;">100.0</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
</table>

#### Parameter Instance: ID

<p>Set CDL_ID. Used to synchronize components, for example with smartMapperGridMap and smartPlannerBreathFirstSearch.
</p>

<table style="border-collapse:collapse;">
<caption>Parameter-Instance: <b>ID</b></caption>
<tr style="background-color:#ccc;">
<th style="border:1px solid black; padding: 5px;"><i>Attribute Name</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Attribute Type</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Attribute Value</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Attribute Description</i></th>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>id</b></td>
<td style="border:1px solid black; padding: 5px;">Int32</td>
<td style="border:1px solid black; padding: 5px;">0</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
</table>

#### Trigger Instance: SAVECURPOS

is-active: <b>false</b>

<p>Save the current robot pose as ?id (for relative movements).
</p>

#### Parameter Instance: SAFETYCL

<p>Set global CDL safety clearance distance [mm]. Robot will keep this distance from obstacles when approaching.
</p>

<table style="border-collapse:collapse;">
<caption>Parameter-Instance: <b>SAFETYCL</b></caption>
<tr style="background-color:#ccc;">
<th style="border:1px solid black; padding: 5px;"><i>Attribute Name</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Attribute Type</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Attribute Value</i></th>
<th style="border:1px solid black; padding: 5px;"><i>Attribute Description</i></th>
</tr>
<tr>
<td style="border:1px solid black; padding: 5px;"><b>safetyClearance</b></td>
<td style="border:1px solid black; padding: 5px;">Int32</td>
<td style="border:1px solid black; padding: 5px;">200</td>
<td style="border:1px solid black; padding: 5px;"></td>
</tr>
</table>

