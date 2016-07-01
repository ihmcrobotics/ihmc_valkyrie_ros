cmake_minimum_required(VERSION 2.8.3)
project(ihmc_valkyrie_ros)

find_package(catkin REQUIRED COMPONENTS
  ihmc_ros_common
  ihmc_msgs
  std_msgs
  geometry_msgs
  message_generation
)

add_message_files(
  FILES
  ValkyrieLowLevelControlModeRosMessage.msg
)

generate_messages(
  DEPENDENCIES
  std_msgs
  ihmc_msgs
)

catkin_package(
)

install(DIRECTORY configurations
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
  PATTERN "*.ini"
  PATTERN "*.yaml"
)

install(DIRECTORY launch
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
  FILES_MATCHING PATTERN "*.launch"
)

include_directories(
  ${catkin_INCLUDE_DIRS}
)
