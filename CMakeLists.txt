# Defines EOS library target.
project( EOS )
cmake_minimum_required( VERSION 2.8.12 )

INCLUDE( VersionMacros )
INCLUDE( SetupTargetMacros )

list( APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/CMakeModules" )

set(CMAKE_EXPORT_COMPILE_COMMANDS "ON")
set(EOS_EGENESIS_JSON "${CMAKE_CURRENT_SOURCE_DIR}/genesis.json" )

#set (ENABLE_INSTALLER 1)
#set (USE_PCH 1)

include(wasm)
if(WASM_TOOLCHAIN)
  message(STATUS "Using WASM clang => " ${WASM_CLANG})
  message(STATUS "Using WASM llc => " ${WASM_LLC})
  message(STATUS "Using WASM llvm-link => " ${WASM_LLVM_LINK})
  add_subdirectory(contracts)
else()
  message(STATUS "-------------------------------------------------------------------")
  message(STATUS "No WASM compiler could be found ... (skiping building of contracts)")
  message(STATUS "-------------------------------------------------------------------")
endif()

add_subdirectory( libraries )
add_subdirectory( programs )
add_subdirectory( plugins )
add_subdirectory( tests )
endif(ENABLE_INSTALLER)
