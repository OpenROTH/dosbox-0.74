add_subdirectory(cpu)
add_subdirectory(debug)
add_subdirectory(dos)
add_subdirectory(fpu)
add_subdirectory(gui)
add_subdirectory(hardware)
add_subdirectory(ints)
add_subdirectory(libs)
add_subdirectory(misc)
add_subdirectory(shell)

set(DOSBOX_SOURCES "${CMAKE_CURRENT_LIST_DIR}/dosbox.cpp")

add_executable(dosbox ${DOSBOX_SOURCES})

target_include_directories(
    dosbox
    PRIVATE
    "${CMAKE_SOURCE_DIR}/include"
    if (MSVC)
    "${CMAKE_SOURCE_DIR}/src/platform/visualc"
    endif(MSVC)
    "${DOSBOX_SDK_DIR}/SDL-1.2.15/include"
)

target_link_libraries(dosbox cpu ddebug dos fpu hardware gui ints misc shell serial gui_tk sdl sdlmain)