cmake_minimum_required(VERSION 3.5)
project(rotors_comm)

# Add support for C++11
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 11)
endif()

find_package(rosidl_default_generators REQUIRED)
find_package(octomap_msgs REQUIRED)
find_package(ament_cmake REQUIRED)
find_package(geometry_msgs REQUIRED)
find_package(std_msgs REQUIRED)
#find_package(cmake_modules REQUIRED)

rosidl_generate_interfaces(${PROJECT_NAME} "srv/Octomap.srv"
  "srv/RecordRosbag.srv" "msg/WindSpeed.msg"
  DEPENDENCIES builtin_interfaces octomap_msgs geometry_msgs std_msgs)

set(INCLUDE_DIRS ${rosidl_default_generators_INCLUDE_DIRS}
  ${octomap_msgs_INCLUDE_DIRS} ${ament_cmake_INCLUDE_DIRS}
  ${geometry_msgs_INCLUDE_DIRS} ${std_msgs_INCLUDE_DIRS}
)
#  ${cmake_modules_INCLUDE_DIRS})

include_directories(${INCLUDE_DIRS})

set(LIBRARY_DIRS ${rosidl_default_generators_LIBRARY_DIRS}
  ${octomap_msgs_LIBRARY_DIRS} ${ament_cmake_LIBRARY_DIRS}
  ${geometry_msgs_LIBRARY_DIRS} ${std_msgs_LIBRARY_DIRS}
)
#  ${cmake_modules_LIBRARY_DIRS})

link_directories(${LIBRARY_DIRS})

set(LIBS ${rosidl_default_generators_LIBRARIES} ${octomap_msgs_LIBRARIES}
  ${ament_cmake_LIBRARIES} ${geometry_msgs_LIBRARIES} ${std_msgs_LIBRARIES}
) # ${cmake_modules_LIBRARIES})

# Declare the service files to be built

ament_export_dependencies(rosidl_default_generators)
ament_export_dependencies(octomap_msgs)
ament_export_dependencies(ament_cmake)
ament_export_dependencies(geometry_msgs)
ament_export_dependencies(std_msgs)
#ament_export_dependencies(cmake_modules)
ament_export_include_directories(${INCLUDE_DIRS})

ament_package()
