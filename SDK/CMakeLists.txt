SET(SKIP_INSTALL_EXPORT TRUE)

#
# ZLIB
#

SET(ZLIB_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/zlib-1.2.11")
ADD_SUBDIRECTORY(${ZLIB_DIRECTORY})

GET_DIRECTORY_PROPERTY(
    ZLIB_BUILD_DIRECTORY
    DIRECTORY
    ${ZLIB_DIRECTORY}
    DEFINITION
    CMAKE_CURRENT_BINARY_DIR
)

GET_DIRECTORY_PROPERTY(
    zlibstatic
    DIRECTORY
    ${ZLIB_DIRECTORY}
    DEFINITION
    zlibstatic
)

SET(ZLIB_LIBRARY zlibstatic)
SET(ZLIB_INCLUDE_DIR ${ZLIB_DIRECTORY})

#
# LIBPNG
#

SET(LIBPNG_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/libpng-1.6.34")

INCLUDE_DIRECTORIES(
    ${ZLIB_DIRECTORY}
    ${ZLIB_BUILD_DIRECTORY}
    ${LIBPNG_DIRECTORY}
    ${LIBPNG_BUILD_DIRECTORY}
)

ADD_SUBDIRECTORY(${LIBPNG_DIRECTORY})

GET_DIRECTORY_PROPERTY(
    LIBPNG_BUILD_DIRECTORY
    DIRECTORY
    ${LIBPNG_DIRECTORY}
    DEFINITION
    CMAKE_CURRENT_BINARY_DIR
)

GET_DIRECTORY_PROPERTY(
    LIBPNG_STATIC
    DIRECTORY
    ${LIBPNG_DIRECTORY}
    DEFINITION
    PNG_LIB_NAME_STATIC
)

SET(ZLIB_DIRECTORY ${ZLIB_DIRECTORY} PARENT_SCOPE)
SET(ZLIB_BUILD_DIRECTORY ${ZLIB_BUILD_DIRECTORY} PARENT_SCOPE)
SET(ZLIB_STATIC zlibstatic PARENT_SCOPE)
SET(LIBPNG_DIRECTORY ${LIBPNG_DIRECTORY} PARENT_SCOPE)
SET(LIBPNG_BUILD_DIRECTORY ${LIBPNG_BUILD_DIRECTORY} PARENT_SCOPE)
SET(LIBPNG_STATIC ${LIBPNG_STATIC} PARENT_SCOPE)

IF(NOT DEFINED DEPS_INCLUDE_DIRECTORIES)
    SET(DEPS_INCLUDE_DIRECTORIES
        ${ZLIB_DIRECTORY}
        ${ZLIB_BUILD_DIRECTORY}
        ${LIBPNG_DIRECTORY}
        ${LIBPNG_BUILD_DIRECTORY}
        PARENT_SCOPE
    )
ELSE()
    LIST(APPEND DEPS_INCLUDE_DIRECTORIES
        ${ZLIB_DIRECTORY}
        ${ZLIB_BUILD_DIRECTORY}
        ${LIBPNG_DIRECTORY}
        ${LIBPNG_BUILD_DIRECTORY}
    )
ENDIF()

#
# SDL
#

set(SDL ${CMAKE_CURRENT_SOURCE_DIR}/sdl-1.2.15)

file(
    GLOB SDL_SOURCES
    ${SDL}/src/*.c
    ${SDL}/src/audio/*.c
    ${SDL}/src/audio/disk/*.c
    ${SDL}/src/audio/dummy/*.c
    ${SDL}/src/cdrom/*.c
    ${SDL}/src/cdrom/dummy/*.c
    ${SDL}/src/cpuinfo/*.c
    ${SDL}/src/events/*.c
    ${SDL}/src/file/*.c
    ${SDL}/src/joystick/*.c
    ${SDL}/src/stdlib/*.c
    ${SDL}/src/thread/*.c
    ${SDL}/src/thread/generic/*.c
    ${SDL}/src/timer/*.c
    ${SDL}/src/video/*.c
    ${SDL}/src/video/dummy/*.c
)

file(
    GLOB SDL_WIN32_SOURCES
    ${SDL}/src/audio/windib/*.c
    ${SDL}/src/audio/windx5/*.c
    ${SDL}/src/cdrom/win32/*.c
    ${SDL}/src/joystick/win32/*.c
    ${SDL}/src/loadso/win32/*.c
    ${SDL}/src/thread/win32/*.c
    ${SDL}/src/timer/win32/*.c
    ${SDL}/src/video/wincommon/*.c
    ${SDL}/src/video/windib/*.c
    ${SDL}/src/video/windx5/*.c
)

file(
    GLOB SDL_MACOS_SOURCES
    ${SDL}/src/audio/macosx/*.c
    ${SDL}/src/cdrom/macosx/*.c
    ${SDL}/src/joystick/darwin/*.c
    ${SDL}/src/loadso/dlopen/*.c
    ${SDL}/src/loadso/macosx/*.c
    # ${SDL}/src/thread/pthread/*.c
    ${SDL}/src/timer/unix/*.c
    ${SDL}/src/video/quartz/*.m
)

set(LIBSDL_SOURCES ${SDL_SOURCES})

if (WIN32)
    set(LIBSDL_SOURCES ${LIBSDL_SOURCES} ${SDL_WIN32_SOURCES})
    set(LIBSDLMAIN_SOURCES ${SDL}/src/main/win32/SDL_win32_main.c)
    file(STRINGS ${SDL}/include/SDL_config.h.default SDL_CONFIG_HEADER)
elseif(UNIX AND APPLE)
    set(LIBSDL_SOURCES ${LIBSDL_SOURCES} ${SDL_MACOS_SOURCES})
    set(LIBSDLMAIN_SOURCES ${SDL}/src/main/macosx/SDLMain.m)
    set(CFLAGS "-Wall -Wextra -O2 -g -fomit-frame-pointer -fPIC")
    set(CXXFLAGS "${CFLAGS} -fno-exceptions -fno-rtti" )
    file(STRINGS ${CMAKE_CURRENT_SOURCE_DIR}/SDL_config.h.macOS SDL_CONFIG_HEADER)
else()
    message(FATAL_ERROR "Unknown operating system-- aborting.")
endif()
string(REPLACE ";" "\n" SDL_CONFIG_HEADER "${SDL_CONFIG_HEADER}")
file(WRITE ${SDL}/include/SDL_config.h "${SDL_CONFIG_HEADER}")

add_library(sdl ${LIBSDL_SOURCES})
target_include_directories(sdl PUBLIC ${SDL}/include)

add_library(sdlmain ${LIBSDLMAIN_SOURCES})
target_include_directories(sdlmain PUBLIC ${SDL}/include)

if (WIN32)
target_link_libraries(sdl dxguid.lib)
endif()

#
# SDLNET
#

set(SDLNET ${CMAKE_CURRENT_SOURCE_DIR}/SDL_net-1.2.8)

file(
    GLOB SDLNET_SOURCES
    ${SDLNET}/*.c
)

set(LIBSDLNET_SOURCES ${SDLNET_SOURCES})

add_library(sdlnet ${LIBSDLNET_SOURCES})
target_include_directories(sdlnet PUBLIC ${SDL}/include)
target_link_libraries(sdlnet Iphlpapi.lib)

#
# PDCURSES
#

add_subdirectory(PDCurses-3.4)