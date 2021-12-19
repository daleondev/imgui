cmake_minimum_required(VERSION 3.0.0)
project(imgui 
    VERSION 0.1.0
    DESCRIPTION "Dear ImGui"
    LANGUAGES CXX)

# ----------------------------------
# preparations
# ----------------------------------

# set cpp standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# sources and headers
file(GLOB SOURCES ${CMAKE_CURRENT_SOURCE_DIR}/*.cpp)
file(GLOB HEADERS ${CMAKE_CURRENT_SOURCE_DIR}/*.h)
set(SOURCES_BACKENDS 
    ${CMAKE_CURRENT_SOURCE_DIR}/backends/imgui_impl_opengl3.cpp 
    ${CMAKE_CURRENT_SOURCE_DIR}/backends/imgui_impl_glut.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/backends/imgui_impl_sdl.cpp)
set(HEADERS_BACKENDS 
    ${CMAKE_CURRENT_SOURCE_DIR}/backends/imgui_impl_opengl3.h 
    ${CMAKE_CURRENT_SOURCE_DIR}/backends/imgui_impl_glut.h
    ${CMAKE_CURRENT_SOURCE_DIR}/backends/imgui_impl_sdl.h)

# linked libraries
set(LIBS SDL2)

# ----------------------------------
# configure library
# ----------------------------------

# static library
add_library(imgui STATIC 
    ${SOURCES} 
    ${HEADERS}
    ${SOURCES_BACKENDS}
    ${HEADERS_BACKENDS})

# include directories
target_include_directories(imgui PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})    

target_link_libraries(imgui PRIVATE ${LIBS})

# runtime library
if(MSVC)
	set_property(TARGET imgui PROPERTY MSVC_RUNTIME_LIBRARY "MultiThreaded$<$<CONFIG:Debug>:Debug>")
endif()
