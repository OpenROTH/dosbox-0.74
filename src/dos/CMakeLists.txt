SET(DOS_SRCS
    dos.cpp
    dos_devices.cpp
    dos_execute.cpp
    dos_files.cpp
    dos_ioctl.cpp
    dos_memory.cpp
    dos_misc.cpp
    dos_classes.cpp
    dos_programs.cpp
    dos_tables.cpp
    drives.cpp
    drives.h
    drive_virtual.cpp
    drive_local.cpp
    drive_cache.cpp
    drive_fat.cpp
    drive_iso.cpp
    dev_con.h
    dos_mscdex.cpp
    dos_keyboard_layout.cpp
    cdrom.h
    cdrom.cpp
    cdrom_ioctl_win32.cpp
    cdrom_aspi_win32.cpp
    cdrom_image.cpp
    cdrom_ioctl_os2.cpp
)

add_library(dos STATIC ${DOS_SRCS})

target_include_directories(
    dos
    PRIVATE
    ${CMAKE_SOURCE_DIR}/include
    if (MSVC)
    "${CMAKE_SOURCE_DIR}/src/platform/visualc"
    endif(MSVC)
    "${DOSBOX_SDK_DIR}/SDL-1.2.15/include"
)

target_link_libraries(dos ddebug)