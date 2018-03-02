add_subdirectory(serialport)

SET(HARDWARE_SRCS
   adlib.cpp
   dma.cpp
   gameblaster.cpp
   hardware.cpp
   iohandler.cpp
   joystick.cpp
   keyboard.cpp
   memory.cpp
   mixer.cpp
   pcspeaker.cpp
   pic.cpp
   sblaster.cpp
   tandy_sound.cpp
   timer.cpp
   vga.cpp
   vga_attr.cpp
   vga_crtc.cpp
   vga_dac.cpp
   vga_draw.cpp
   vga_gfx.cpp
   vga_other.cpp
   vga_memory.cpp
   vga_misc.cpp
   vga_seq.cpp
   vga_xga.cpp
   vga_s3.cpp
   vga_tseng.cpp
   vga_paradise.cpp
   cmos.cpp
   disney.cpp
   gus.cpp
   mpu401.cpp
   ipx.cpp
   ipxserver.cpp
   dbopl.cpp
)

add_library(hardware STATIC ${HARDWARE_SRCS})
target_include_directories(
    hardware
    PRIVATE
    ${CMAKE_SOURCE_DIR}/include
    if (MSVC)
    "${CMAKE_SOURCE_DIR}/src/platform/visualc"
    endif(MSVC)
    "${DOSBOX_SDK_DIR}/SDL-1.2.15/include"
    "${DOSBOX_SDK_DIR}/SDL_net-1.2.8/"
    ${DEPS_INCLUDE_DIRECTORIES}
)

target_link_libraries(hardware debug winmm.lib ${ZLIB_STATIC} ${LIBPNG_STATIC} sdlnet)