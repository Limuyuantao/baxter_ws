# cartesian_planner
This package includes Cartesian planners for Baxter.
There are multiple cartesian-plan options, including:

*specify start and end poses w/rt base.  Only orientation of end pose will be considered; orientation of start pose is ignored;
planned motion keeps orientation constant while moving in a straight line from start position to end position.

*specify start as a q_vec, and goal as a Cartesian pose (w/rt base).  Orientation of goal pose will be obtained quickly,
then preserved through the linear move.

*specify start as a q_vec, and desired delta-p Cartesian motion while holding R fixed at initial orientation

## Example usage


The desired motion is specified hard-coded in the main program
to maintain orientation of the tool flange pointing up while translating at y-desired, z-desired from x-start to x-end.
These values can be edited to test alternative motions.

There are corresponding example mains for baxter.

This package also hosts action servers for cartesian moves for baxter right arm.
These present a generic interface that can be driven by a generic action client.
It is necessary to run a launch file to publish transforms from specific, named frames on robots (e.g.
right_hand to generic_gripper_frame and torso to system_ref_frame, etc).  These launch files are in the launch
sub-directory.

For Baxter robot:
`roslaunch baxter_gazebo baxter_world.launch`
wait for start-up, then enable the actuators:
`rosrun baxter_tools enable_robot.py -e`
Start a trajectory-interpolation action server:
`rosrun baxter_trajectory_streamer rt_arm_as`
start the generic static transforms:
`roslaunch cartesian_planner baxter_static_transforms.launch`
start the cartesian-motion action server for Baxter's right arm:
`rosrun  cartesian_planner baxter_rt_arm_cart_move_as` 
start a generic action client:
`rosrun cartesian_planner example_generic_cart_move_ac` 




