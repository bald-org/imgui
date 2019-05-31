cmake_minimum_required(VERSION 3.14)

project(imgui)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(DEBUG_COMPILE_FLAGS -fsanitize=leak -pedantic -Wall -Wextra -Wnon-virtual-dtor -Werror -Wcast-align -Wunused -Woverloaded-virtual -Wpedantic -Wconversion -Wnull-dereference -Wdouble-promotion -Wduplicated-cond -Wduplicated-branches -Wlogical-op -g)
set(RELEASE_COMPILE_FLAGS -Ofast -Werror)

include_directories(${CMAKE_CURRENT_SOURCE_DIR})

add_library(imgui
        ${CMAKE_CURRENT_SOURCE_DIR}/imgui_widgets.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/imgui_draw.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/imgui_demo.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/imgui.cpp)

if(DEFINE_DEBUG)
    target_compile_options(imgui PUBLIC ${DEBUG_COMPILE_FLAGS})
elseif(DEFINE_RELEASE)
    target_compile_options(imgui PUBLIC ${RELEASE_COMPILE_FLAGS})
endif()