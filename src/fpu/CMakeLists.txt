SET(FPU_SRCS
   fpu.cpp
   fpu_instructions.h
   fpu_instructions_x86.h
)

add_library(fpu STATIC ${FPU_SRCS})

target_include_directories(
    fpu
    PRIVATE
    ${CMAKE_SOURCE_DIR}/include
    if (MSVC)
    "${CMAKE_SOURCE_DIR}/src/platform/visualc"
    endif(MSVC)
)