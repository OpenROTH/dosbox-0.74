SET(SHELL_SRCS
   shell.cpp
   shell_batch.cpp
   shell_cmds.cpp
   shell_misc.cpp
)

add_library(shell STATIC ${SHELL_SRCS})

target_include_directories(
    shell
    PRIVATE
    ${CMAKE_SOURCE_DIR}/include
    if (MSVC)
    "${CMAKE_SOURCE_DIR}/src/platform/visualc"
    endif(MSVC)
)

target_link_libraries(shell ddebug)