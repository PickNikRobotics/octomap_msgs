cmake_minimum_required(VERSION 3.5)
project(octomap_msgs)

# Default to C++14
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Wextra -Wpedantic")
endif()

find_package(ament_cmake REQUIRED)
find_package(rosidl_default_generators REQUIRED)
find_package(std_msgs REQUIRED)
find_package(geometry_msgs REQUIRED)

include_directories(include)

add_message_files(
  DIRECTORY msg
  FILES Octomap.msg OctomapWithPose.msg
  )

add_service_files(
  DIRECTORY srv
  FILES GetOctomap.srv BoundingBoxQuery.srv
)

generate_messages(DEPENDENCIES std_msgs geometry_msgs)

catkin_package(DEPENDS message_runtime geometry_msgs std_msgs
               INCLUDE_DIRS include
)

install(DIRECTORY include/
        DESTINATION include
        FILES_MATCHING PATTERN "*.h"
        PATTERN ".svn" EXCLUDE)
