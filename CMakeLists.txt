cmake_minimum_required (VERSION 3.0)
project (SCDBG)

add_compile_options(-std=c++14)

include_directories(core/libelfin core/linenoise include)
add_executable(scdbg src/main.cpp core/linenoise/linenoise.c)

add_custom_target(
   libelfin
   COMMAND make
   WORKING_DIRECTORY ${PROJECT_SOURCE_DIR}/core/libelfin
)
target_link_libraries(scdbg
                      ${PROJECT_SOURCE_DIR}/core/libelfin/dwarf/libdwarf++.so
                      ${PROJECT_SOURCE_DIR}/core/libelfin/elf/libelf++.so)
add_dependencies(scdbg libelfin)