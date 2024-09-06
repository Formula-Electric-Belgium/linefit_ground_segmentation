cmake_minimum_required(VERSION 2.8.3)
project(linefit_ground_segmentation)

# find_package(catkin_simple 0.1.0 REQUIRED )

# catkin_simple(ALL_DEPS_REQUIRED)

add_definitions(-std=c++14)
find_package(catkin REQUIRED COMPONENTS
	roscpp
	eigen_conversions
	tf2_ros
)

find_package(PCL REQUIRED)

catkin_package(
  INCLUDE_DIRS include
  # LIBRARIES path_planning CATKIN_DEPENDS feb_msgs rospy visualization_msgs
  # DEPENDS system_lib
)

include_directories(${PCL_INCLUDE_DIRS}
	include
	include/${PROJECT_NAME}
	${catkin_INCLUDE_DIRS}
)

link_directories(${PCL_LIBRARY_DIRS})
add_definitions(${PCL_DEFINITIONS})

add_executable(ground_segmentation_node src/ground_segmentation_node.cc src/ground_segmentation.cc src/segment.cc src/bin.cc src/viewer.cc)
add_executable(ground_segmentation_test_node src/ground_segmentation_test_node.cc src/ground_segmentation.cc src/segment.cc src/bin.cc src/viewer.cc)
target_link_libraries(ground_segmentation_node ${catkin_LIBRARIES} ${PCL_LIBRARIES})
target_link_libraries(ground_segmentation_test_node ${catkin_LIBRARIES} ${PCL_LIBRARIES})


#############
# QTCREATOR #
#############
FILE(GLOB_RECURSE LibFiles "include/*")
add_custom_target(headers SOURCES ${LibFiles})
