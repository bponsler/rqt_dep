cmake_minimum_required(VERSION 2.8.3)
project(rqt_dep)

# Add support for C++11
if(NOT WIN32)
  add_definitions(-std=c++11)
endif()

find_package(ament_cmake REQUIRED)
find_package(ament_cmake_python REQUIRED)

ament_python_install_package(${PROJECT_NAME})

set(INCLUDE_DIRS ${ament_cmake_INCLUDE_DIRS})
include_directories(${INCLUDE_DIRS})

set(LIBRARY_DIRS ${ament_cmake_LIBRARY_DIRS})

link_directories(${LIBRARY_DIRS})

set(LIBS ${ament_cmake_LIBRARIES})

# Load all dependencies required for this package

if(BUILD_TESTING)
  find_package(ament_cmake_nose REQUIRED)
  ament_add_nose_test(rqt_dep_nose_tests test/dotcode_pack_test.py)
endif()

install(FILES plugin.xml DESTINATION share/${PROJECT_NAME})

install(DIRECTORY resource DESTINATION share/${PROJECT_NAME})

install(PROGRAMS scripts/rqt_dep DESTINATION bin)

ament_export_dependencies(ament_cmake)
ament_export_include_directories(${INCLUDE_DIRS})

ament_package()
