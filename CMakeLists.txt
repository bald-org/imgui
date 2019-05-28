cmake_minimum_required(VERSION 3.14)

project(imgui)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)

include_directories(${CMAKE_CURRENT_SOURCE_DIR})

add_library(imgui
            ${CMAKE_CURRENT_SOURCE_DIR}/imgui_widgets.cpp
            ${CMAKE_CURRENT_SOURCE_DIR}/imgui_draw.cpp
            ${CMAKE_CURRENT_SOURCE_DIR}/imgui_demo.cpp
            ${CMAKE_CURRENT_SOURCE_DIR}/imgui.cp)

