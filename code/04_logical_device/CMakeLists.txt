cmake_minimum_required(VERSION 3.0)

project(craft LANGUAGES C CXX)

set(CMAKE_CXX_STANDARD 17)

add_executable(
    04_logical_device
    04_logical_device.cpp
)


find_package(Vulkan REQUIRED)
add_dependencies(04_logical_device Vulkan::Vulkan)

set(VULKAN_LIBRARIES "Vulkan::Vulkan")

# using PkgConfig to determine how to link against
# the system's glfw and curl
find_package(PkgConfig REQUIRED)
pkg_check_modules(GLFW REQUIRED glfw3)

include_directories(${GLFW_INCLUDE_DIR} ${Vulkan_INCLUDE_DIR} deps/stb/)


target_link_libraries(04_logical_device dl m pthread
  ${GLFW_LIBRARIES} ${VULKAN_LIBRARIES})



# Install
install(TARGETS 04_logical_device DESTINATION bin)
