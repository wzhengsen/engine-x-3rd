cmake_minimum_required(VERSION 3.6)

set(lib_name mojoal)
set(target_name ${lib_name})

project(${lib_name})

add_library(${target_name} STATIC
  mojoal.c
)

include(../cmake/CocosExternalConfig.cmake)

target_include_directories(${target_name} PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include)
target_compile_definitions(${target_name} PUBLIC AL_LIBTYPE_STATIC=1)

set_target_properties(${target_name}
    PROPERTIES
    ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib"
    LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib"
    FOLDER "External"
)

