cmake_minimum_required(VERSION 2.8.3)
project(pviz)

set(CMAKE_BUILD_TYPE Release)

find_package(Boost REQUIRED)
include_directories(${Boost_INCLUDE_DIRS})

find_package(catkin REQUIRED
             COMPONENTS
                geometry_msgs
                kdl_parser
                orocos_kdl
                roscpp
                tf
                trajectory_msgs
                visualization_msgs)
include_directories(${catkin_INCLUDE_DIRS})

include_directories(include)

catkin_package(INCLUDE_DIRS include
               CATKIN_DEPENDS
                   geometry_msgs
                   kdl_parser
                   orocos_kdl
                   tf
                   trajectory_msgs
                   visualization_msgs
               DEPENDS Boost
               LIBRARIES ${PROJECT_NAME})

add_library(${PROJECT_NAME} src/pviz.cpp)
target_link_libraries(${PROJECT_NAME} ${catkin_LIBRARIES})

add_executable(pvizExample src/pviz_example.cpp)
target_link_libraries(pvizExample ${PROJECT_NAME})
