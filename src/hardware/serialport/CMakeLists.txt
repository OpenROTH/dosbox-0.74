SET(SERIAL_SRCS
   directserial.cpp
   directserial.h
   libserial.cpp
   libserial.h
   serialdummy.cpp
   serialdummy.h
   serialport.cpp
   softmodem.cpp
   softmodem.h
   misc_util.cpp
   misc_util.h
   nullmodem.cpp
   nullmodem.h
)

add_library(serial STATIC ${SERIAL_SRCS})

target_include_directories(
    serial
    PRIVATE
    ${CMAKE_SOURCE_DIR}/include
    if (MSVC)
    "${CMAKE_SOURCE_DIR}/src/platform/visualc"
    endif(MSVC)
    "${DOSBOX_SDK_DIR}/SDL-1.2.15/include"
    "${DOSBOX_SDK_DIR}/SDL_net-1.2.8/"
)

target_link_libraries(serial debug ws2_32.lib sdlnet)