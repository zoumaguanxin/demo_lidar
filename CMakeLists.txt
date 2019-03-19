cmake_minimum_required(VERSION 2.8.0)

project(demo_lidar)


find_package(catkin REQUIRED COMPONENTS
		 std_msgs
		 roscpp
		 nav_msgs
		 sensor_msgs
		 geometry_msgs
		 tf2
                 pcl_conversions
                 tf
                 cv_bridge
		 )

#set the default path for built executables to the "bin" directory
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
#set the default path for built libraries to the "lib" directory
set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)


SET(CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake)
find_package(Eigen3 REQUIRED)

find_package(PCL 1.2 REQUIRED)
find_package(OpenCV REQUIRED)

include_directories(${catkin_INCLUDE_DIRS} ${PCL_INCLUDE_DIRS} ${OpenCV_INCLUDE_DIRS})
include_directories("${PROJECT_SOURCE_DIR}/include")

add_subdirectory(isamlib)
link_libraries(isamlib)


add_executable(featureTracking src/featureTracking.cpp)
target_link_libraries(featureTracking  ${Boost_LIBRARIES} ${catkin_LIBRARIES}  ${PCL_LIBRARIES} ${OpenCV_LIBRARIES})

 
add_executable(visualOdometry src/visualOdometry.cpp)
target_link_libraries(visualOdometry ${Boost_LIBRARIES} ${catkin_LIBRARIES} ${PCL_LIBRARIES} ${OpenCV_LIBRARIES})
 
add_executable(bundleAdjust src/bundleAdjust.cpp)
target_link_libraries(bundleAdjust ${Boost_LIBRARIES} ${catkin_LIBRARIES} ${PCL_LIBRARIES} ${OpenCV_LIBRARIES})

 add_executable(processDepthmap src/processDepthmap.cpp)
target_link_libraries(processDepthmap ${Boost_LIBRARIES} ${catkin_LIBRARIES} ${PCL_LIBRARIES} ${OpenCV_LIBRARIES})
 
 add_executable(stackDepthPoint src/stackDepthPoint.cpp)
 target_link_libraries(stackDepthPoint ${Boost_LIBRARIES} ${catkin_LIBRARIES} ${PCL_LIBRARIES} ${OpenCV_LIBRARIES})

 add_executable(transformMaintenance src/transformMaintenance.cpp)
 target_link_libraries(transformMaintenance ${Boost_LIBRARIES} ${catkin_LIBRARIES} ${PCL_LIBRARIES} ${OpenCV_LIBRARIES})
 
 add_executable(registerPointCloud src/registerPointCloud.cpp) 
 target_link_libraries(registerPointCloud ${Boost_LIBRARIES} ${catkin_LIBRARIES} ${PCL_LIBRARIES} ${OpenCV_LIBRARIES})
