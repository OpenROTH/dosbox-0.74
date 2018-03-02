cmake_minimum_required(VERSION 3.0)

set(DOSBOX_VERSION_MAJOR 0)
set(DOSBOX_VERSION_MINOR 74)

project(DOSBOX VERSION ${DOSBOX_VERSION_MAJOR}.${DOSBOX_VERSION_MINOR})

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

#foreach(sdkproj "enet" "minhook" "mbedtls")
#    if ((NOT EXISTS "${CMAKE_SOURCE_DIR}/SDK/${sdkproj}/.git"))
#        message(SEND_ERROR "The git submodules are not available. Please run git submodule update --init --recursive")
#    endif()
#endforeach(sdkproj)

if("${CMAKE_GENERATOR}" MATCHES "Win64")
    set(IS_64BIT_BUILD TRUE)
else()
    set(IS_64BIT_BUILD FALSE)
endif()

set(DOSBOX_SRC_DIR "${CMAKE_CURRENT_LIST_DIR}/src")
set(DOSBOX_SDK_DIR "${CMAKE_CURRENT_LIST_DIR}/SDK")

# satisfy find_package(ZLIB REQUIRED)
#set(ZLIB_ROOT <zlib folder here>)

# SDK project generation
add_subdirectory("${CMAKE_SOURCE_DIR}/SDK/")

# DOS BOX
add_subdirectory(src)