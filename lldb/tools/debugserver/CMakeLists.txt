cmake_minimum_required(VERSION 3.4.3)

project(Debugserver LANGUAGES C CXX ASM-ATT)

if (CMAKE_SOURCE_DIR STREQUAL CMAKE_CURRENT_SOURCE_DIR)
  set(CMAKE_MODULE_PATH
    ${CMAKE_MODULE_PATH}
    "${CMAKE_SOURCE_DIR}/../../cmake"
    "${CMAKE_SOURCE_DIR}/../../cmake/modules"
    )

  include(LLDBStandalone)
  include(debugserverConfig)
  include(AddLLDB)

  # debugserver contains ObjC++ code, so let's disable Clang modules
  # in this subdirectory to avoid building ObjC++ modules (which often
  # doesn't properly work).
  remove_module_flags()

  set(LLDB_SOURCE_DIR "${CMAKE_SOURCE_DIR}/../../")
  include_directories(${LLDB_SOURCE_DIR}/include)
endif()

add_subdirectory(source)
