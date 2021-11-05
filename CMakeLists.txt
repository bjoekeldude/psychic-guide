cmake_minimum_required(VERSION 3.16)

set(PROJECT_NAME psychic_guide)
set(CMAKE_CXX_STANDARD 17)

project(${PROJECT_NAME})
add_library(${PROJECT_NAME} SHARED)

target_compile_definitions(${PROJECT_NAME} PRIVATE _USE_MATH_DEFINES=1)

target_sources(${PROJECT_NAME} PRIVATE source/library.cpp)
target_sources(${PROJECT_NAME} PUBLIC source/library.h)

set_target_properties(${PROJECT_NAME} PROPERTIES
    ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/build/lib"
    LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/build/lib"
    RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/build/bin"
)

find_package(Boost)
if(Boost_FOUND)
  message(STATUS "Found Boost")
  target_include_directories(${PROJECT_NAME} PRIVATE ${Boost_INCLUDE_DIRS})
  # didn't link against boost, since for the most part it's header only.
endif()
