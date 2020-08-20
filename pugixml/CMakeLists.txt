cmake_minimum_required(VERSION 3.14)

set(lib_name pugixml)
set(target_name ext_${lib_name})

project(${lib_name})

include(../cmake/CocosExternalConfig.cmake)

set(${target_name}_src
  pugixml.cpp
)
add_library(${target_name} STATIC
  ${${target_name}_src}
)
target_include_directories(${target_name} PRIVATE .)
set_target_properties(${target_name}
  PROPERTIES
  ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib"
  LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib"
  FOLDER "External"
)

set_target_properties(${target_name} PROPERTIES
  INTERFACE_INCLUDE_DIRECTORIES "${CMAKE_CURRENT_SOURCE_DIR}"
)
