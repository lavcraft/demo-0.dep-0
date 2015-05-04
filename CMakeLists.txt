cmake_minimum_required(VERSION 2.8)

project(dep0)

set(CMAKE_MODULE_PATH ${dep0_SOURCE_DIR}/cmake)

include(DetermineVersion)

set(SOURCES dep0.cpp)
set(HEADERS dep0.h)

add_library(dep0 ${HEADERS} ${SOURCES})

# Set up our version.
set(proj0_VERSION_MAJOR   "1")
set(proj0_VERSION_MINOR   "2")
set(proj0_VERSION_PATCH   "2")
set(proj0_VERSION
  "${proj0_VERSION_MAJOR}.${proj0_VERSION_MINOR}.${proj0_VERSION_PATCH}")
find_package(Git)
determine_version(${dep0_SOURCE_DIR} ${GIT_EXECUTABLE} "proj0")

install(FILES ${HEADERS}
   DESTINATION "${INSTALL_INCLUDE_DIR}/dep0")
     
ADD_CUSTOM_COMMAND(
   OUTPUT ${CMAKE_BINARY_DIR}/dep0.h
   COMMAND ${CMAKE_COMMAND} -E copy ${CMAKE_CURRENT_SOURCE_DIR}/dep0.h
${CMAKE_BINARY_DIR}/dep0.h
   DEPENDS ${CMAKE_CURRENT_SOURCE_DIR}/dep0.h
   )
