cmake_minimum_required(VERSION 3.5)
project(interfaces)

# Ensure the C++ standard is set (C++14 or higher)
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()

# Compiler flags for GNU/Clang
if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# Find necessary ROS 2 packages
find_package(ament_cmake REQUIRED)
find_package(ament_cmake_python REQUIRED)
find_package(rosidl_default_generators REQUIRED)
find_package(rclcpp REQUIRED)
find_package(rclcpp_action REQUIRED)
find_package(rclcpp_components REQUIRED)
find_package(std_msgs REQUIRED)
find_package(nav_msgs REQUIRED)
find_package(geometry_msgs REQUIRED)

# Generate interfaces (messages, services, actions)
rosidl_generate_interfaces(${PROJECT_NAME}
  "msg/Numnew.msg"
  "srv/AddThreeInts.srv"
  "srv/GetTarget.srv"
  "srv/SaveStatus.srv"
  "action/Fibonacci.action"
  "action/ExecutePath.action"
  "action/GetPath.action"
  DEPENDENCIES geometry_msgs nav_msgs std_msgs
)

# Export dependencies needed for this package
ament_export_dependencies(rosidl_default_runtime)

# Declare and package the ament package
ament_package()