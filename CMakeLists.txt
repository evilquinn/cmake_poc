cmake_minimum_required(VERSION 3.5)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++14 -Wall -Wextra")
set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS} -O0 -g3")

option(ENABLE_COVERAGE "Enable code coverage metrics for debug builds" OFF)
if ( ${ENABLE_COVERAGE} )
    set(CMAKE_CXX_FLAGS_DEBUG
        "${CMAKE_CXX_FLAGS_DEBUG} -ftest-coverage -fprofile-arcs -pg")
endif()

set(CMAKE_INSTALL_PREFIX "$\{CMAKE_CURRENT_BINARY_DIR}")

include_directories(${CMAKE_SOURCE_DIR}/src)

set(EXPORT_DIR ${CMAKE_BINARY_DIR}/export)
set(EXPORT_LIB_DIR ${EXPORT_DIR}/lib)
set(EXPORT_INCLUDE_DIR ${EXPORT_DIR}/include)

add_library ( exported_headers INTERFACE )
#set_property(TARGET exported_headers PROPERTY IMPORT_PREFIX .)

install(EXPORT cmake_poc_export DESTINATION ${CMAKE_BINARY_DIR})

add_subdirectory(src)

enable_testing()
