cmake_minimum_required(VERSION 3.5)
project(executor_comparison)

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

find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(std_msgs REQUIRED)

add_executable(single_thread ./src/single_thread.cpp)
ament_target_dependencies(single_thread
	rclcpp
	std_msgs)

add_executable(multi_thread ./src/multi_thread.cpp)
ament_target_dependencies(multi_thread
	rclcpp
	std_msgs)

install(TARGETS
	single_thread
	DESTINATION lib/${PROJECT_NAME})

install(TARGETS
	multi_thread
	DESTINATION lib/${PROJECT_NAME})

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  ament_lint_auto_find_test_dependencies()
endif()

ament_package()
