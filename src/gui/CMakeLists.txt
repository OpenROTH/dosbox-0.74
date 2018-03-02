SET(GUI_SRCS
   sdlmain.cpp
   sdl_mapper.cpp
   dosbox_logo.h
   render.cpp
   render_scalers.cpp
   render_scalers.h
   render_templates.h
   render_loops.h
   render_simple.h
   render_templates_sai.h
   render_templates_hq.h
   render_templates_hq2x.h
   render_templates_hq3x.h
   midi.cpp
   midi_win32.h
   midi_oss.h
   midi_coreaudio.h
   midi_alsa.h
   midi_coremidi.h
   sdl_gui.cpp
   dosbox_splash.h
)

add_library(gui STATIC ${GUI_SRCS})

target_include_directories(
    gui
    PRIVATE
    ${CMAKE_SOURCE_DIR}/include
    if (MSVC)
    "${CMAKE_SOURCE_DIR}/src/platform/visualc"
    endif(MSVC)
    "${DOSBOX_SDK_DIR}/SDL-1.2.15/include"
)

target_link_libraries(gui debug winmm.lib opengl32.lib)