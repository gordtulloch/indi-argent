cmake_minimum_required(VERSION 3.5)
project(indi_argent C CXX)

list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake_modules/")
list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/../cmake_modules/")
include(GNUInstallDirs)

set(INDI_ARGENT_VERSION_MAJOR 1)
set(INDI_ARGENT_VERSION_MINOR 0)

find_package(INDI REQUIRED)

configure_file(${CMAKE_CURRENT_SOURCE_DIR}/config.h.cmake              ${CMAKE_CURRENT_BINARY_DIR}/config.h)
configure_file(${CMAKE_CURRENT_SOURCE_DIR}/indi_argent.xml.cmake   ${CMAKE_CURRENT_BINARY_DIR}/indi_argent.xml)

include_directories(${CMAKE_CURRENT_BINARY_DIR})
include_directories(${CMAKE_CURRENT_SOURCE_DIR})
include_directories(${INDI_INCLUDE_DIR})

include(CMakeCommon)

set(indiargent_SRCS
   ${CMAKE_CURRENT_SOURCE_DIR}/indi-argent.cpp
)

add_executable(indi_argent ${indiargent_SRCS})

target_link_libraries(indi_argent ${INDI_LIBRARIES} crypt)

install(TARGETS indi_agent RUNTIME DESTINATION bin )
install(FILES ${CMAKE_CURRENT_BINARY_DIR}/indi_agent.xml DESTINATION ${INDI_DATA_DIR})






