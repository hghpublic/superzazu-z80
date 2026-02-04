cmake_minimum_required(VERSION 4.2)

project(z80 C)


set(target z80)
add_library(${target} STATIC
    z80.c
    z80.h
)

set(target z80_tests)
add_executable(${target}
    z80_tests.c
)
target_link_libraries(${target} PRIVATE z80)

# copy roms

add_custom_command(TARGET ${target} POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_directory 
        ${CMAKE_CURRENT_SOURCE_DIR}/roms
        $<TARGET_FILE_DIR:${target}>/roms)
