cmake_minimum_required(VERSION 3.14)
project(SLPF)

set(CMAKE_CXX_STANDARD 14)

set(PROJECT_SOURCE_DIR src)

include_directories(3rd_party)
include_directories(freeglut/include)

message("Platform: " "${CMAKE_SIZEOF_VOID_P}*8")

IF(CMAKE_SIZEOF_VOID_P EQUAL 8)  # x64
    link_directories(freeglut/lib/x64)
ELSE(CMAKE_SIZEOF_VOID_P EQUAL 8)  # x86
    link_directories(freeglut/lib)
ENDIF(CMAKE_SIZEOF_VOID_P EQUAL 8)

add_executable(SLPF src/main.cpp
                    src/toolkit.hpp
                    src/core.h
                    src/core.cpp)

target_link_libraries(SLPF freeglut opengl32 glu32)

IF(CMAKE_SIZEOF_VOID_P EQUAL 8)  # x64
    file(COPY freeglut/bin/x64/freeglut.dll DESTINATION ${PROJECT_BINARY_DIR})
ELSE(CMAKE_SIZEOF_VOID_P EQUAL 8)  # x86
    file(COPY freeglut/bin/freeglut.dll DESTINATION ${PROJECT_BINARY_DIR})
ENDIF(CMAKE_SIZEOF_VOID_P EQUAL 8)