list(APPEND WIN32_SOURCES
     pdcclip.c
     pdcdisp.c
     pdcgetsc.c
     pdckbd.c
     pdcscrn.c
     pdcsetsc.c
     pdcutil.c)
foreach(file ${WIN32_SOURCES})
  list(APPEND MAINWIN32_SOURCES ${CMAKE_CURRENT_SOURCE_DIR}/${file})
endforeach()
set(MAINWIN32_SOURCES ${MAINWIN32_SOURCES} PARENT_SCOPE)