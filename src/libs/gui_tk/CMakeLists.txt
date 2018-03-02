SET(GUI_TK_SRCS
   gui_tk.cpp
   gui_tk.h
)

add_library(gui_tk STATIC ${GUI_TK_SRCS})

target_include_directories(
    gui_tk
    PRIVATE
    ${CMAKE_SOURCE_DIR}/include
    #if (MSVC)
    #"${CMAKE_SOURCE_DIR}/src/platform/visualc"
    #endif(MSVC)
    #"${DOSBOX_SDK_DIR}/SDL-1.2.15/include"
)