cmake_minimum_required(VERSION 2.8.3)
project(example_robot_interface)

find_package(catkin_simple REQUIRED)
find_package(Eigen3)

#find_package(irb120_ik REQUIRED)
#find_package(example_joint_space_planner REQUIRED)

# this is depreciated but still necessary for now.
if(NOT EIGEN3_FOUND)
  # Fallback to cmake_modules
  find_package(cmake_modules REQUIRED)
  find_package(Eigen REQUIRED)
  set(EIGEN3_INCLUDE_DIRS ${EIGEN_INCLUDE_DIR})
  set(EIGEN_DEP Eigen)
  # message("Found Eigen ${EIGEN_INCLUDE_DIR}")
  # Possibly map additional variables to the EIGEN3_ prefix.
else()
  set(EIGEN3_INCLUDE_DIRS ${EIGEN3_INCLUDE_DIR})
  set(EIGEN_DEP Eigen3)
  # message("Found Eigen3 ${EIGEN3_INCLUDE_DIR}")
endif()
add_definitions(${EIGEN_DEFINITIONS})
#old...update for Eigen3
#find_package(Eigen REQUIRED)
#include_directories(${Eigen_INCLUDE_DIRS})
#add_definitions(${EIGEN_DEFINITIONS})

catkin_simple()

# example boost usage
# find_package(Boost REQUIRED COMPONENTS system thread)

# C++0x support - not quite the same as final C++11!
SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++0x")

# Libraries
# cs_add_libraries(my_lib src/my_lib.cpp)   

# Executables
cs_add_executable(example_robot_interface src/example_robot_interface.cpp)
cs_add_executable(test_traj_sender src/test_traj_sender.cpp)
cs_add_executable(test_traj_sin_sender src/test_traj_sin_sender.cpp)
#cs_add_executable(test_traj_point_sender src/test_traj_point_sender.cpp)
#cs_add_executable(test_abby_sender src/test_abby_sender.cpp)
#cs_add_executable(test_abby_sender2 src/test_abby_sender2.cpp)
#cs_add_executable(test_ik_traj_sender src/test_ik_traj_sender.cpp)
#cs_add_executable(test_ik_traj_sender2 src/test_ik_traj_sender2.cpp)

#target_link_libraries(test_ik_traj_sender2 irb120_ik) #don't need this; already referenced in package.xml
# target_link_library(example my_lib)

cs_install()
cs_export()
    
