SET(DEBUG_SRCS
    debug.cpp
    debug_disasm.cpp
    debug_gui.cpp
    debug_win32.cpp
)

add_library(ddebug STATIC ${DEBUG_SRCS})

target_include_directories(
    ddebug
    PRIVATE
    ${CMAKE_SOURCE_DIR}/include
    if (MSVC)
    "${CMAKE_SOURCE_DIR}/src/platform/visualc"
    endif(MSVC)
    "${DOSBOX_SDK_DIR}/SDL-1.2.15/include"
    "${DOSBOX_SDK_DIR}/PDCurses-3.4"
)

target_link_libraries(ddebug sdl pdcurses)