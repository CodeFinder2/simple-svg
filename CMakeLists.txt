cmake_minimum_required(VERSION 3.12)
project("svg_writer" VERSION 1.0.0
  DESCRIPTION "Header-only library for C++11 to write SVG images programmatically"
  HOMEPAGE_URL "https://github.com/CodeFinder2/simple-svg")
include(GNUInstallDirs)

add_library(${PROJECT_NAME} INTERFACE)
target_include_directories(
  ${PROJECT_NAME}
  INTERFACE $<BUILD_INTERFACE:${${PROJECT_NAME}_SOURCE_DIR}/include>
            $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>)
target_compile_features(${PROJECT_NAME} INTERFACE cxx_std_11)

option(SIMPLE_SVG_BUILD_EXAMPLE "Build the SimpleSVG example binary?" OFF)
if (SIMPLE_SVG_BUILD_EXAMPLE)
  add_executable(${PROJECT_NAME}_example src/main.cpp)
  target_link_libraries(${PROJECT_NAME}_example ${PROJECT_NAME})
  target_compile_options(${PROJECT_NAME}_example PRIVATE -Wall -Wextra -Werror -pedantic -Wshadow)
endif()

install(DIRECTORY ${PROJECT_SOURCE_DIR}/include/${PROJECT_NAME} DESTINATION include)
