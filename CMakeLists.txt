cmake_minimum_required(VERSION 3.14)

project(imgui)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
if(NOT WINDOWS_BUILD)
    set(DEBUG_COMPILE_FLAGS -fsanitize=leak -g)
    set(RELEASE_COMPILE_FLAGS -Ofast)
endif()

include_directories(${CMAKE_CURRENT_SOURCE_DIR})
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/../glfw/include)
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/../glad/include)

add_definitions(-DIMGUI_IMPL_OPENGL_LOADER_GLAD)

add_library(imgui
        ${CMAKE_CURRENT_SOURCE_DIR}/imgui_widgets.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/imgui_draw.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/imgui_demo.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/imgui.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/examples/imgui_impl_opengl3.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/examples/imgui_impl_glfw.cpp)

if(NOT WINDOWS_BUILD)
    if(DEFINE_DEBUG)
        target_compile_options(imgui PUBLIC ${DEBUG_COMPILE_FLAGS})
    elseif(DEFINE_RELEASE)
        target_compile_options(imgui PUBLIC ${RELEASE_COMPILE_FLAGS})
    endif()
endif()
