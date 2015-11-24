cmake_minimum_required(VERSION 2.4.6)
include($ENV{ROS_ROOT}/core/rosbuild/rosbuild.cmake)

# Set the build type.  Options are:
#  Coverage       : w/ debug symbols, w/o optimization, w/ code-coverage
#  Debug          : w/ debug symbols, w/o optimization
#  Release        : w/o debug symbols, w/ optimization
#  RelWithDebInfo : w/ debug symbols, w/ optimization
#  MinSizeRel     : w/o debug symbols, w/ optimization, stripped binaries
#set(ROS_BUILD_TYPE RelWithDebInfo)

rosbuild_init()

SET(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${YARP_MODULE_PATH})

FIND_PACKAGE(YARP)

#set(CMAKE_BINARY_DIR ${CMAKE_CURRENT_SOURCE_DIR}/build)
SET(CMAKE_LIBRARY_PATH ${CMAKE_LIBRARY_PATH} /usr/local/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/build/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/build/bin)
#AUX_SOURCE_DIRECTORY(${CMAKE_CURRENT_SOURCE_DIR}/src MY_SOURCE_FILES)


       
#add include directories
INCLUDE_DIRECTORIES(${YARP_INCLUDE_DIRS} "${CMAKE_CURRENT_SOURCE_DIR}/include")
INCLUDE_DIRECTORIES(${CMAKE_CURRENT_BINARY_DIR})

LINK_DIRECTORIES($CMAKE_LIBRARY_PATH)


#set the default path for built executables to the "bin" directory
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
#set the default path for built libraries to the "lib" directory
set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)

#uncomment if you have defined messages
rosbuild_genmsg()
#uncomment if you have defined services
#rosbuild_gensrv()


#rosbuild_add_library(${PROJECT_NAME} src/example.cpp)
#target_link_libraries(${PROJECT_NAME} another_library)
#rosbuild_add_boost_directories()
#rosbuild_link_boost(${PROJECT_NAME} thread)
#rosbuild_add_executable(data_wrapper src/main.cpp)#${MY_SOURCE_FILES})
#rosbuild_add_executable(extractor src/extractor.cpp)
rosbuild_add_executable(IntTacMain src/IntTacMain.cpp)

#need YARP LIBRARY for streaming CyberGlove/Texscan
#target_link_libraries(data_wrapper ${YARP_LIBRARIES})
target_link_libraries(IntTacMain ${YARP_LIBRARIES})
