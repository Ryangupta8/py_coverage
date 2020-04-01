cmake_minimum_required(VERSION 2.8.3)
project(py_coverage)	

add_compile_options(-std=c++11)

## Find catkin macros and libraries
## if COMPONENTS list like find_package(catkin REQUIRED COMPONENTS xyz)
## is used, also find other catkin packages
find_package(catkin REQUIRED COMPONENTS
  roscpp
  rospy
  geometry_msgs
  sensor_msgs
  message_generation
  std_msgs
  std_srvs
  tf
)

find_package(Boost REQUIRED)
find_package(Eigen3 QUIET)

if(NOT EIGEN3_FOUND)
    find_package(PkgConfig REQUIRED)
    pkg_check_modules(EIGEN3 REQUIRED eigen3)
    set(EIGEN3_INCLUDE_DIR ${EIGEN3_INCLUDE_DIRS})
endif()


# add_service_files(
#    FILES
# )

catkin_python_setup()

catkin_package(
  INCLUDE_DIRS include/${PROJECT_NAME}
  CATKIN_DEPENDS 
   roscpp
   rospy
   geometry_msgs
   sensor_msgs
   std_msgs
   message_runtime
   tf
  DEPENDS
   Boost
 )

include_directories(
  include/${PROJECT_NAME}
  src
  ${catkin_INCLUDE_DIRS}
  ${Boost_INCLUDE_DIRS}
  ${EIGEN3_INCLUDE_DIR}
)

SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")



install(DIRECTORY scripts/
    DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
    USE_SOURCE_PERMISSIONS
)

