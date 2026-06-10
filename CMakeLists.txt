cmake_minimum_required(VERSION 3.5)
project(pairs_vins_imu_filter)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(LIBRARIES 
  PairsVinsImuFilter_VinsImuFilter
  )

set(CATKIN_DEPENDENCIES
  cmake_modules
  geometry_msgs
  pairs_lib
  nav_msgs
  nodelet
  roscpp
  tf2
  tf2_ros
  )

find_package(catkin REQUIRED COMPONENTS
  ${CATKIN_DEPENDENCIES}
)

catkin_package(
  LIBRARIES ${LIBRARIES}
  CATKIN_DEPENDS ${CATKIN_DEPENDENCIES}
)

include_directories(
  ${catkin_INCLUDE_DIRS}
)

add_library(PairsVinsImuFilter_VinsImuFilter
  src/VinsImuFilter.cpp
  )

add_dependencies(PairsVinsImuFilter_VinsImuFilter
  ${${PROJECT_NAME}_EXPORTED_TARGETS}
  ${catkin_EXPORTED_TARGETS}
)

target_link_libraries(PairsVinsImuFilter_VinsImuFilter
  ${catkin_LIBRARIES}
)

## --------------------------------------------------------------
## |                           Install                          |
## --------------------------------------------------------------

install(TARGETS ${LIBRARIES}
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_GLOBAL_BIN_DESTINATION}
  )

install(DIRECTORY config launch
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
  )

install(FILES nodelets.xml
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
  )
