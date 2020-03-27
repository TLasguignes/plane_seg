cmake_minimum_required(VERSION 2.6.0)

project(plane_seg_ros)

add_compile_options(-std=c++1y -Wall)
#add_definitions(-std=c++1y -Wall)

find_package(catkin REQUIRED COMPONENTS
  eigen_conversions
  pcl_conversions
  tf_conversions
  pcl_ros
  grid_map_core
  grid_map_ros
  grid_map_msgs
  plane_seg
)

find_package(OpenCV 3.0 QUIET)
find_package(PCL 1.7.2 REQUIRED) # Test

catkin_package(
  INCLUDE_DIRS
    #include
  CATKIN_DEPENDS eigen_conversions pcl_conversions tf_conversions pcl_ros plane_seg
)


include_directories(
#  include
  ${catkin_INCLUDE_DIRS}
  ${PCL_INCLUDE_DIRS} # Test
)

link_directories(${PCL_LIBRARY_DIRS}) # Test
add_definitions(${PCL_DEFINITIONS}) # Test

set(APP_NAME plane_seg_ros)
add_executable(${APP_NAME} src/${APP_NAME}.cpp)
target_link_libraries(${APP_NAME} boost_system ${catkin_LIBRARIES})

add_executable(plane_seg_ri src/plane_seg_ri.cpp)
target_link_libraries(plane_seg_ri boost_system ${catkin_LIBRARIES} ${PCL_LIBRARIES})
