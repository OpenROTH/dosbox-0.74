cmake_minimum_required(VERSION 3.0)

set(DOSBOX_VERSION_MAJOR 0)
set(DOSBOX_VERSION_MINOR 74)

project(DOSBOX VERSION ${DOSBOX_VERSION_MAJOR}.${DOSBOX_VERSION_MINOR})

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

#
# TODO : Print warning, never tested under win64
#
if("${CMAKE_GENERATOR}" MATCHES "Win64")
    set(IS_64BIT_BUILD TRUE)
else()
    set(IS_64BIT_BUILD FALSE)
endif()

set(DOSBOX_SRC_DIR "${CMAKE_CURRENT_LIST_DIR}/src")
set(DOSBOX_SDK_DIR "${CMAKE_CURRENT_LIST_DIR}/SDK")

# SDK project generation
add_subdirectory("${CMAKE_SOURCE_DIR}/SDK/")

# DOS BOX
add_subdirectory(src)