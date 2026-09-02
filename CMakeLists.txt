cmake_minimum_required(VERSION 3.10)
project(asio)

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_CURRENT_BINARY_DIR}/lib")
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "${CMAKE_CURRENT_BINARY_DIR}/lib")
set(CMAKE_PDB_OUTPUT_DIRECTORY     "${CMAKE_CURRENT_BINARY_DIR}/bin")
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_CURRENT_BINARY_DIR}/bin")


set(HDRS
  include/asio.hpp
)

set(SRCS
  src/asio.cpp
  )

if (UNIX)
set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -std=c++11")
set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} -std=c++11")
endif (UNIX)

source_group("Header Files" FILES ${HDRS})
source_group("Source Files" FILES ${SRCS})

add_definitions(-DASIO_SEPARATE_COMPILATION)
if (WIN32)
#add_definitions(-D_WIN32_WINNT=0x0601) # Windows 7
add_definitions(-D_WIN32_WINNT=0x0A00) # Windows 10
endif (WIN32)

add_library(asio STATIC ${HDRS} ${SRCS})

target_include_directories(asio
  PUBLIC
  ${CMAKE_CURRENT_SOURCE_DIR}/include/
  )
