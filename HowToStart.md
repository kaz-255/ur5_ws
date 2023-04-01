#Note on using the test Python Program

##   Launching Gazebo Simulation
To start the simulation:
-  Download all the files into a folder
    It is probably best to have the `ur5_ws` folder directly under `$HOME` of the linux directory.
    
    Open the folder in terminal by for example `right click -> Open in Terminal`, or use `cd ur5_ws`
___
1.  Start Terminal #1 
    Type the following command 

        source devel/setup.bash
        roslaunch ur_gazebo ur5_bringup.launch

    This should start a Gazebo simulation with nothing but the UR5 model inside it. I've yet to know how to spawn extra item inside the world.

___
2. Start Terminal #2
    Run the following command
        
        roslaunch ur5_moveit_config moveit_planning_execution.launch sim:=true

    This enables planningfor the robotic arm in simulation
___
3.  Start terminal #3
    Type the following command
    
        roslaunch ur5_moveit_config moveit_rviz.launch
    This launches the Rviz program

##   Executing the program

The following executes a Python Program that the tutors uploaded to Moodle and modified to execute some pre-set actions (move to specific locations in the cartesian cooordinates). 

Type the command
    
    source ~/ur5_ws/devel/setup.bash
    rosrun move0 move0.py

Note that in the Termianl there will be messages such as "Press enter to execute a movement using [mode]". 

The robot will first reset to a horizonal position (note that when the Gazebo world starts the robot is in a 'limped' position that appears to be straight but was not), after the first enter it should go to position


___
##  File and discussion
You may find/edit the Python Program in `ur5_ws/src/move0/src`. In particular, observe and change the `go_to_pose(x, y ,z)` and `go_to_joint_state(0,0,0,0,0,60)` parameters and see how it might work differently. From my own observations the move to joint state is a forward operation (meaning we explicitly specify the angle of each joint), while the `move_to_pose` appears to be an 'inverse' kinematics.

A few problem is yet to be solved, such as 
- Sometimes when using go_to_pose() the robot end effector may not be able to go to the specified point, or go half way and fails, or goes there in a very funny trajectory