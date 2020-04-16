# coordinator

Top-level node that is a client of: object_grabber, and object_finder.
Waits for an incoming goal, then starts entire process of: 
recognition of object, grasp of object, and dropoff of object.

The client specifies the object of interest, optionally with a specified pose 
(alternatively, requesting Kinect-based perception of the object).  The client
specifies the object's drop-off pose.  Grasp transforms are associated with
specified object ID's (via an object-properties library).

start up an empty world:
`roslaunch gazebo_ros empty_world.launch`
 
 spawn Baxter on pedestal in front of a table and a block:
 `roslaunch baxter_variations baxter_on_pedestal_w_kinect.launch`

launch multiple nodes, including trajectory streamers, cartesian planner, rviz, baxter-playfile, triad_display (for object-frame visualization), object-grabber, object-finder coordinator, and block-state resetter:
`roslaunch coordinator coord_vision_manip.launch`
(to try object_grabber v2, run: roslaunch coordinator coord_vision_manip2.launch)
(also, v2 will respond to the client: rosrun coordinator example_cart_move_client,
which will induce a Cartesian gripper motion to a specified goal pose)

Command the robot to: find the table height, find the block on the table, compute an approach and grasp strategy,
execute the plan, and retract (holding the block) to the pre-pose position.
`rosrun coordinator acquire_block_client`

(to straddle the block, run: rosrun coordinator straddle_block_client)

The block can be placed back down again with the node:
`rosrun coordinator dropoff_block_client`


