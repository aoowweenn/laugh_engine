cmake_minimum_required(VERSION 3.0 FATAL_ERROR)

#set(CMAKE_CXX_STANDARD 1z)
#set(CMAKE_CXX_STANDARD_REQUIRED ON)
add_compile_options("-std=c++1z")

project(LaughEngine)

find_package(Threads REQUIRED)
find_package(Vulkan REQUIRED)
find_package(glfw3 REQUIRED)
#find_package(assimp)
#find_package(glm 0.9.8)

include_directories(${CMAKE_SOURCE_DIR}/include)
include_directories(${CMAKE_SOURCE_DIR}/include/gli)

set(ASSIMP_LIB_DIR ${CMAKE_SOURCE_DIR}/lib/assimp)
link_directories(${ASSIMP_LIB_DIR})

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/bin)

add_executable(${PROJECT_NAME} main.cpp)
target_link_libraries(${PROJECT_NAME} Threads::Threads Vulkan::Vulkan glfw assimp)

add_custom_command(
    TARGET ${PROJECT_NAME}
    POST_BUILD
    COMMAND ln;-fs;${ASSIMP_LIB_DIR}/libassimp.so;${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/libassimp.so.3
) 