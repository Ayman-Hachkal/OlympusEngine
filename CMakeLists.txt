cmake_minimum_required(VERSION 3.15)

set(CMAKE_CXX_STANDARD 23)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

project(Olympus VERSION 1.0 LANGUAGES CXX)

include(cmake/CPM.cmake)

if(NOT DEFINED ENV{VULKAN_SDK})
    file(GLOB VULKAN_SDK_PATHS "$ENV{HOME}/VulkanSDK/*/macOS")
    if(VULKAN_SDK_PATHS)
        list(GET VULKAN_SDK_PATHS -1 VULKAN_SDK_PATH)
        set(Vulkan_ROOT ${VULKAN_SDK_PATH})
    endif()
endif()

find_package(Vulkan REQUIRED)
CPMAddPackage("gh:glfw/glfw#3.4")
CPMAddPackage("gh:g-truc/glm#1.0.1")

add_executable(${PROJECT_NAME} src/main.cpp)
target_link_libraries(${PROJECT_NAME} Vulkan::Vulkan glfw glm)
