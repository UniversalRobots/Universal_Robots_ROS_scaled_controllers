cmake_minimum_required(VERSION 3.0.2)
project(speed_scaling_interface)

## Find catkin macros and libraries
## if COMPONENTS list like find_package(catkin REQUIRED COMPONENTS xyz)
## is used, also find other catkin packages
find_package(catkin REQUIRED COMPONENTS
  hardware_interface
  roscpp
)

include_directories(
  include
  ${catkin_INCLUDE_DIRS}
)

catkin_package(
  INCLUDE_DIRS include
  CATKIN_DEPENDS
    hardware_interface
    roscpp
  )


#############
## Install ##
#############

# Mark cpp header files for installation
install(DIRECTORY include/${PROJECT_NAME}/
  DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
  FILES_MATCHING PATTERN "*.h"
  PATTERN ".svn" EXCLUDE
)
