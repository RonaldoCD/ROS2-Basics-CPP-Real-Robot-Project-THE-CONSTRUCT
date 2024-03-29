cmake_minimum_required(VERSION 3.5)
project(wall_follower)

# Default to C99
if(NOT CMAKE_C_STANDARD)
  set(CMAKE_C_STANDARD 99)
endif()

# Default to C++14
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(rclcpp_action REQUIRED)
find_package(std_msgs REQUIRED)
find_package(nav_msgs REQUIRED)
find_package(sensor_msgs REQUIRED)
find_package(geometry_msgs REQUIRED)
find_package(custom_interfaces REQUIRED)

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  # the following line skips the linter which checks for copyrights
  # uncomment the line when a copyright and license is not present in all source files
  #set(ament_cmake_copyright_FOUND TRUE)
  # the following line skips cpplint (only works in a git repo)
  # uncomment the line when this package is not in a git repo
  #set(ament_cmake_cpplint_FOUND TRUE)
  ament_lint_auto_find_test_dependencies()
endif()

add_executable(wall_follower_node src/wall_follower.cpp)
ament_target_dependencies(wall_follower_node rclcpp std_msgs nav_msgs sensor_msgs geometry_msgs)

add_executable(wall_finder_node src/wall_finder.cpp)
ament_target_dependencies(wall_finder_node rclcpp std_msgs nav_msgs sensor_msgs geometry_msgs custom_interfaces)

add_executable(wall_follower_node_part2 src/wall_follower_part2.cpp)
ament_target_dependencies(wall_follower_node_part2 rclcpp std_msgs nav_msgs sensor_msgs geometry_msgs custom_interfaces)

add_executable(wall_follower_node_part3 src/wall_follower_part3.cpp)
ament_target_dependencies(wall_follower_node_part3 rclcpp std_msgs nav_msgs sensor_msgs geometry_msgs custom_interfaces rclcpp_action)

add_executable(odom_recorder_server_node src/odom_recorder_server.cpp)
ament_target_dependencies(odom_recorder_server_node rclcpp std_msgs nav_msgs sensor_msgs geometry_msgs custom_interfaces rclcpp_action)

# add_executable(odom_recorder_client_node src/odom_recorder_server.cpp)
# ament_target_dependencies(odom_recorder_server_node rclcpp std_msgs nav_msgs sensor_msgs geometry_msgs custom_interfaces rclcpp_action)

install(TARGETS
   wall_follower_node
   wall_finder_node
   wall_follower_node_part2
   wall_follower_node_part3
   odom_recorder_server_node
#    odom_recorder_client_node
   
   DESTINATION lib/${PROJECT_NAME}
 )

# Install launch files.
install(DIRECTORY
  launch
  DESTINATION share/${PROJECT_NAME}/
)

ament_package()
