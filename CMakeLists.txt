cmake_minimum_required(VERSION 2.8.3)
project(frame_for_ros)

set(CMAKE_BUILD_TYPE "Release")
set(CMAKE_CXX_FLAGS "-std=c++14")

set(CMAKE_CXX_FLAGS_RELEASE "-O3 -Wall -g -pthread")

include_directories(${CMAKE_CURRENT_SOURCE_DIR})

find_package(catkin REQUIRED COMPONENTS
    tf
    roscpp
    rospy
    
    pcl_conversions
    eigen_conversions
    
    std_msgs
    sensor_msgs
    geometry_msgs
    nav_msgs
    message_generation
    visualization_msgs
)

# add_messageE_files(
#     DIRECTORY msg
#     FILES
# )

# add_service_files(
#    DIRECTORY srv
#    FILES 
# )

catkin_package(
    INCLUDE_DIRS include
    DEPENDS PCL

    CATKIN_DEPENDS
    std_msgs
    nav_msgs
    geometry_msgs
    sensor_msgs
    message_runtime
    message_generation
    roscpp
)

include_directories(
    include
    ${catkin_INCLUDE_DIRS}
    ${PCL_INCLUDE_DIRS}
    ${OpenCV_INCLUDE_DIRS}
    # ${GTSAM_LIBRARY_DIRS}
)
link_directories(
    include
    ${PCL_LIBRARIES_DIRS}
    ${OpenCV_LIBRARY_DIRS}
)

add_executable(${PROJECT_NAME}_main src/main.cpp)
add_dependencies(${PROJECT_NAME}_main ${catkin_EXPORTED_TARGETS} ${PROJECT_NAME}__generate_messages_cpp)
target_link_libraries(${PROJECT_NAME}_main ${catkin_LIBRARIES} ${PCL_LIBRARIES})
# target_link_libraries(${PROJECT_NAME}_main ${catkin_LIBRARIES})