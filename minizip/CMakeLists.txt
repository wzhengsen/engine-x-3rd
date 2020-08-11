cmake_minimum_required(VERSION 3.14)

set(lib_name minizip)
set(target_name ext_${lib_name})

project(${lib_name})

set(${target_name}_src
  ioapi.cpp
  unzip.cpp
  zip.cpp
  ioapi_mem.cpp
)

add_library(${target_name} STATIC
  ${${target_name}_src}
)

target_include_directories(${target_name}
  PRIVATE ${COCOS2DX_ROOT_PATH}/cocos
  PUBLIC .
  )
target_compile_definitions(${target_name} PRIVATE CC_STATIC)

if(MACOSX OR ANDROID OR WINDOWS)
  get_target_property(zlib_header ext_zlib INTERFACE_INCLUDE_DIRECTORIES)
  target_include_directories(${target_name} PUBLIC ${zlib_header}
)
endif()

target_link_libraries(${target_name}
  ext_zlib
)

if(MSVC)
target_compile_definitions(${target_name} PRIVATE _CRT_SECURE_NO_WARNINGS)
endif()

set_target_properties(${target_name}
    PROPERTIES
    ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib"
    LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib"
    FOLDER "External"
)
