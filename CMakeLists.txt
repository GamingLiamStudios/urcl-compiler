cmake_minimum_required(VERSION 3.9)
project(urcl-compiler)

if(NOT MSVC)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -march=native")
endif()

set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/${PROJECT_NAME})
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/${PROJECT_NAME})

add_subdirectory(extern)

set(SOURCE_FILES
    source/main.cpp

    source/token.cpp
    source/compiler.cpp
)

add_executable(${PROJECT_NAME} ${SOURCE_FILES})

target_compile_features(${PROJECT_NAME} PUBLIC cxx_std_17)

target_include_directories(${PROJECT_NAME} PUBLIC "extern")
target_include_directories(${PROJECT_NAME} PUBLIC "source") # to allow paths relative to project root

target_link_libraries(${PROJECT_NAME} PRIVATE fmt)
