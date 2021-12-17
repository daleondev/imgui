cmake_minimum_required(VERSION 3.0.0)
project(imgui VERSION 0.1.0)

# set cpp standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# pic
if(UNIX)
	set(CMAKE_POSITION_INDEPENDENT_CODE ON)
endif()

# sources and headers
file(GLOB SOURCES ${CMAKE_CURRENT_SOURCE_DIR}/*.cpp)
file(GLOB HEADERS ${CMAKE_CURRENT_SOURCE_DIR}/*.h)

# shared library
add_library(imgui SHARED 
    ${SOURCES} 
    ${HEADERS})
    
# runtime library
if(MSVC)
	set_property(TARGET glew PROPERTY MSVC_RUNTIME_LIBRARY "MultiThreaded$<$<CONFIG:Debug>:Debug>")
endif()
