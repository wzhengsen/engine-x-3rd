cmake_minimum_required(VERSION 3.6)

set(lib_name openssl)

project(${lib_name})

include(../cmake/CocosExternalConfig.cmake)

# -----macro: set openssl sub target-----
macro(set_openssl_sub_target sub_lib_name)

  set(sub_target_name ext_${sub_lib_name})
  if(WINDOWS)
    add_library(${sub_target_name} SHARED IMPORTED GLOBAL)
  else()
    add_library(${sub_target_name} STATIC IMPORTED GLOBAL)
  endif()

  set_target_properties(${sub_target_name} PROPERTIES
    INTERFACE_INCLUDE_DIRECTORIES "${CMAKE_CURRENT_SOURCE_DIR}/include/${platform_name}"
  )
  if(WINDOWS)
    set_target_properties(${sub_target_name} PROPERTIES
      IMPORTED_LOCATION "${platform_spec_path}/lib${sub_lib_name}-1_1-x64.dll"
      IMPORTED_IMPLIB "${platform_spec_path}/lib${sub_lib_name}.lib"
    )
  else()
    set_target_properties(${sub_target_name} PROPERTIES
      IMPORTED_LOCATION "${platform_spec_path}/lib${sub_lib_name}.a"
    )
  endif()
endmacro()

# -----macro: set openssl sub target-----
macro(set_openssl_sub_target_dll sub_lib_name)
  if(WINDOWS)
    set(sub_target_name ext_${sub_lib_name})
    add_library(${sub_target_name} SHARED IMPORTED GLOBAL)
    set_target_properties(${sub_target_name} PROPERTIES
      INTERFACE_INCLUDE_DIRECTORIES "${CMAKE_CURRENT_SOURCE_DIR}/include/${platform_name}"
    )
    set_target_properties(${sub_target_name} PROPERTIES
      IMPORTED_LOCATION "${platform_spec_path}/${sub_lib_name}.dll"
      IMPORTED_IMPLIB "${platform_spec_path}/libssl.lib"
    )
  endif()
endmacro()


# -----sub target 1: ssl-----
set(target_name ssl)
set_openssl_sub_target(${target_name})

# -----sub target 2: crypto-----
set(target_name crypto)
set_openssl_sub_target(${target_name})

# -----sub target 3: libeay32-----
set(target_name libeay32)
set_openssl_sub_target_dll(${target_name})

# -----sub target 4: ssleay32-----
set(target_name ssleay32)
set_openssl_sub_target_dll(${target_name})