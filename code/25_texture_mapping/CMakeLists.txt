cmake_minimum_required(VERSION 3.0)

project(craft LANGUAGES C CXX)

set(CMAKE_CXX_STANDARD 17)


add_executable(
    25_texture_mapping
    25_texture_mapping.cpp
)


set(demo_shaders
        ../25_shader_textures.frag
        ../25_shader_textures.vert
)


find_package(Vulkan REQUIRED)
add_dependencies(25_texture_mapping Vulkan::Vulkan)

set(VULKAN_LIBRARIES "Vulkan::Vulkan")

# using PkgConfig to determine how to link against
# the system's glfw and curl
find_package(PkgConfig REQUIRED)
pkg_check_modules(GLFW REQUIRED glfw3)

include_directories(${GLFW_INCLUDE_DIR} ${Vulkan_INCLUDE_DIR} ../../deps/stb/)


target_link_libraries(25_texture_mapping dl m pthread
  ${GLFW_LIBRARIES} ${VULKAN_LIBRARIES})


set(SHADERS_DIR "${CMAKE_SOURCE_DIR}/../")
set(OUTPUT_COPY_DIR ${CMAKE_CURRENT_BINARY_DIR})


add_custom_command(TARGET 25_texture_mapping PRE_BUILD
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

    add_custom_command(TARGET 25_texture_mapping POST_BUILD DEPENDS ${demo_shaders}
        COMMAND ${CMAKE_BINARY_DIR}/CompileShaders.sh
        )
endif()



# Install
install(TARGETS 25_texture_mapping DESTINATION bin)

install(DIRECTORY ${CMAKE_BINARY_DIR}/shaders/ DESTINATION shaders/)
install(DIRECTORY ../../resources/ DESTINATION resources/)
install(DIRECTORY ../../images/ DESTINATION textures/)
