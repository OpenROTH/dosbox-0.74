SET(INTS_SRCS
   mouse.cpp
   xms.cpp
   xms.h
   ems.cpp
   int10.cpp
   int10.h
   int10_char.cpp
   int10_memory.cpp
   int10_misc.cpp
   int10_modes.cpp
   int10_vesa.cpp
   int10_pal.cpp
   int10_put_pixel.cpp
   int10_video_state.cpp
   int10_vptable.cpp
   bios.cpp
   bios_disk.cpp
   bios_keyboard.cpp
)

add_library(ints STATIC ${INTS_SRCS})

target_include_directories(
    ints
    PRIVATE
    ${CMAKE_SOURCE_DIR}/include
    if (MSVC)
    "${CMAKE_SOURCE_DIR}/src/platform/visualc"
    endif(MSVC)
    "${DOSBOX_SDK_DIR}/SDL-1.2.15/include"
)

target_link_libraries(ints ddebug)