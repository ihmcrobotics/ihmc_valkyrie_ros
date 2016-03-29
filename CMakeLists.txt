cmake_minimum_required(VERSION 2.8.3)
project(ihmc_valkyrie_ros)

find_package(catkin REQUIRED COMPONENTS
  ihmc_ros_common
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
