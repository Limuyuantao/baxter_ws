cmake_minimum_required(VERSION 2.8.3)
project(cartesian_planner)

find_package(catkin_simple REQUIRED)

#uncomment next line to use OpenCV library
#find_package(OpenCV REQUIRED)
#uncomment the next 2 lines to use the point-cloud library
#find_package(PCL 1.7 REQUIRED)
#include_directories(${PCL_INCLUDE_DIRS})


#uncomment the following 4 lines to use the Eigen library
find_package(cmake_modules REQUIRED)
find_package(Eigen3 REQUIRED)
include_directories(${EIGEN3_INCLUDE_DIR})
add_definitions(${EIGEN_DEFINITIONS})

catkin_simple()

# example boost usage
# find_package(Boost REQUIRED COMPONENTS system thread)

# C++0x support - not quite the same as final C++11!
# use carefully;  can interfere with point-cloud library
# SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++0x")

# Libraries: uncomment the following and edit arguments to create a new library
#cs_add_library(cartesian_planner src/cartesian_planner.cpp) 
 
#cartesian planners specialized for various target arms: 
cs_add_library(baxter_cartesian_planner src/baxter_cartesian_planner.cpp) 


#examples using cartesian-planning libraries in main functions:
cs_add_executable(example_baxter_cart_path_planner src/example_baxter_cart_path_planner_main.cpp)



#cartesian-move action service nodes specialized for target robots
cs_add_executable(baxter_rt_arm_cart_move_as src/baxter_rt_arm_cart_move_as.cpp)


# Executables: uncomment the following and edit arguments to compile new nodes
# may add more of these lines for more nodes from the same package
# cs_add_executable(example src/example.cpp)



#target_link_libraries(plan_playfile cartesian_planner ${catkin_LIBRARIES})

target_link_libraries(example_baxter_cart_path_planner baxter_cartesian_planner ${catkin_LIBRARIES})

#target_link_libraries(baxter_cart_move_as baxter_cartesian_planner ${catkin_LIBRARIES})

#link action servers w/ respective planner libraries
target_link_libraries(baxter_rt_arm_cart_move_as baxter_cartesian_planner ${catkin_LIBRARIES})


#target_link_libraries(baxter_cart_move_action_client baxter_arm_motion_commander ${catkin_LIBRARIES})
#target_link_libraries(baxter_cart_move_action_client2 baxter_arm_motion_commander ${catkin_LIBRARIES})
#target_link_libraries(baxter_cart_move_action_client3 baxter_arm_motion_commander ${catkin_LIBRARIES})
#target_link_libraries(baxter_cart_move_action_client_w_gripper baxter_arm_motion_commander ${catkin_LIBRARIES})


#action clients can be generic--robot independent
cs_add_library(cart_motion_commander src/cart_motion_commander.cpp) 
cs_add_executable(example_generic_cart_move_ac src/example_generic_cart_move_ac.cpp)
target_link_libraries(example_generic_cart_move_ac cart_motion_commander ${catkin_LIBRARIES})

cs_install()
cs_export()
    
