SET(CPU_SRCS
    callback.cpp
    cpu.cpp
    flags.cpp
    modrm.cpp
    modrm.h
    core_full.cpp
    instructions.h
    paging.cpp
    lazyflags.h
    core_normal.cpp
    core_simple.cpp
    core_prefetch.cpp
    core_dyn_x86.cpp
    core_dynrec.cpp
)

add_library(cpu STATIC ${CPU_SRCS})

target_include_directories(
    cpu
    PRIVATE
    ${CMAKE_SOURCE_DIR}/include
    if (MSVC)
    "${CMAKE_SOURCE_DIR}/src/platform/visualc"
    endif(MSVC)
)