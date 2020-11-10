cmake_minimum_required(VERSION 3.0.2)
project(beginner_tutorials)

## Find catkin and any catkin packages
find_package(catkin REQUIRED COMPONENTS roscpp rospy std_msgs genmsg)

## Declare ROS messages and services
add_message_files(DIRECTORY msg FILES Num.msg)
add_service_files(DIRECTORY srv FILES AddTwoInts.srv)

## Generate added messages and services
generate_messages(DEPENDENCIES std_msgs)

## Declare a catkin package
catkin_package(
   CATKIN_DEPENDS message_runtime
)
## Build talker and listener
include_directories(include ${catkin_INCLUDE_DIRS})

add_executable(talker src/talker.cpp)
target_link_libraries(talker ${CATKIN_PACKAGE_SHARE_DESTINATION})
add_dependencies(talker beginner_tutorials_generate_messages_cpp)

add_executable(listener src/listener.cpp)
target_link_libraries(listener ${CATKIN_PACKAGE_SHARE_DESTINATION})
add_dependencies(listener beginner_tutorials_generate_messages_cpp)

install(FILES
  talker
  listener
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
)
