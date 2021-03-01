cmake_minimum_required(VERSION 3.0)

project(craft LANGUAGES C CXX)

set(CMAKE_CXX_STANDARD 17)

add_executable(
    16_swap_chain_recreation
    16_swap_chain_recreation.cpp
)


set(demo_shaders
        ../09_shader_base.frag
        ../09_shader_base.vert
)


find_package(Vulkan REQUIRED)
add_dependencies(16_swap_chain_recreation Vulkan::Vulkan)

set(VULKAN_LIBRARIES "Vulkan::Vulkan")

# using PkgConfig to determine how to link against
# the system's glfw and curl
find_package(PkgConfig REQUIRED)
pkg_check_modules(GLFW REQUIRED glfw3)

include_directories(${GLFW_INCLUDE_DIR} ${Vulkan_INCLUDE_DIR} )


target_link_libraries(16_swap_chain_recreation dl m pthread
  ${GLFW_LIBRARIES} ${VULKAN_LIBRARIES})


set(SHADERS_DIR "${CMAKE_SOURCE_DIR}/../")
set(OUTPUT_COPY_DIR ${CMAKE_CURRENT_BINARY_DIR})


add_custom_command(TARGET 16_swap_chain_recreation PRE_BUILD
    COMMAND mkdir "${OUTPUT_COPY_DIR}/shaders"
    COMMAND cp "${SHADERS_DIR}/*.vert" "${SHADERS_DIR}/*.frag" "${OUTPUT_COPY_DIR}/shaders" || :
)



if(WIN32)
STRING(REGEX REPLACE "/" "\\\\" SHADERS_DIR ${SHADERS_DIR})
endif()
if(WIN32)
    configure_file(./shaders/CompileShaders.bat.in ${CMAKE_BINARY_DIR}/CompileShaders.bat @ONLY)

    add_custom_command(TARGET Shaders POST_BUILD DEPENDS ${demo_shaders}
        COMMAND ${CMAKE_BINARY_DIR}/CompileShaders.bat
        )
else()
    configure_file(../CompileShaders.sh.in ${CMAKE_BINARY_DIR}/CompileShaders.sh @ONLY)

    add_custom_command(TARGET 16_swap_chain_recreation POST_BUILD DEPENDS ${demo_shaders}
        COMMAND ${CMAKE_BINARY_DIR}/CompileShaders.sh
        )
endif()



# Install
install(TARGETS 16_swap_chain_recreation DESTINATION bin)

install(DIRECTORY ${CMAKE_BINARY_DIR}/shaders/ DESTINATION shaders/)
install(DIRECTORY ../../resources/ DESTINATION resources/)
