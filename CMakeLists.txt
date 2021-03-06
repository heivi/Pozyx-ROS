cmake_minimum_required(VERSION 2.8.3)
project(pozyx)
find_package(catkin REQUIRED roscpp std_msgs geometry_msgs sensor_msgs message_generation)

# only needed for RPI
find_package(Threads REQUIRED)

add_message_files(
  FILES
	StringStamped.msg
)

generate_messages(
  DEPENDENCIES
	std_msgs
)

catkin_package(
	INCLUDE_DIRS include
	CATKIN_DEPENDS message_runtime
)

include_directories(include ${Boost_INCLUDE_DIRS} ${catkin_INCLUDE_DIRS})
add_executable(pozyx src/pozyx.cpp)
add_library(pozyx-lib include/Pozyx-custom-library/Pozyx_core.cpp include/Pozyx-custom-library/Pozyx_lib.cpp include/Pozyx-custom-library/helpers.cpp)

#for RPI
target_link_libraries(pozyx pozyx-lib pigpiod_if2 rt)

#for LINUX
#target_link_libraries(pozyx pozyx-lib)

target_link_libraries(pozyx
        ${catkin_LIBRARIES}
)

# the rest only needed for RPI
if(THREADS_HAVE_PTHREAD_ARG)
  target_compile_options(PUBLIC pozyx "-pthread")
endif()
if(CMAKE_THREAD_LIBS_INIT)
  target_link_libraries(pozyx "${CMAKE_THREAD_LIBS_INIT}")
endif()


#set(CMAKE_CXX_FLAGS "-std=c++11 ${CMAKE_CXX_FLAGS}")
