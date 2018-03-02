SET(MISC_SRCS
   cross.cpp
   messages.cpp
   programs.cpp
   setup.cpp
   support.cpp
)

add_library(misc STATIC ${MISC_SRCS})

target_include_directories(
    misc
    PRIVATE
    ${CMAKE_SOURCE_DIR}/include
    if (MSVC)
    "${CMAKE_SOURCE_DIR}/src/platform/visualc"
    endif(MSVC)
)