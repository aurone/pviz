cmake_minimum_required(VERSION 2.8.3)
project(pviz)

set(CMAKE_BUILD_TYPE Release)

find_package(Boost REQUIRED)

find_package(catkin REQUIRED
    COMPONENTS
        geometry_msgs
        kdl_parser
        roscpp
        tf
        trajectory_msgs
        visualization_msgs)

find_package(orocos_kdl REQUIRED)

catkin_package(
    INCLUDE_DIRS
        include
    CATKIN_DEPENDS
        geometry_msgs
        kdl_parser
        tf
        trajectory_msgs
        visualization_msgs
    DEPENDS
        boost
        orocos_kdl
    LIBRARIES
        ${PROJECT_NAME})

include_directories(${Boost_INCLUDE_DIRS})
include_directories(${catkin_INCLUDE_DIRS})
include_directories(${orocos_kdl_INCLUDE_DIRS})
include_directories(include)

add_library(${PROJECT_NAME} src/pviz.cpp)
target_link_libraries(${PROJECT_NAME} ${catkin_LIBRARIES})

add_executable(pvizExample src/pviz_example.cpp)
target_link_libraries(pvizExample ${PROJECT_NAME})

install(TARGETS ${PROJECT_NAME} pvizExample
        ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
        LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
        RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION})
