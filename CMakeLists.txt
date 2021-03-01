cmake_minimum_required(VERSION 3.0)

project(craft LANGUAGES C CXX)

set(CMAKE_CXX_STANDARD 17)


add_executable(
    00_base_code
    code/00_base_code.cpp
)

add_executable(
    01_instance_creation
    code/01_instance_creation.cpp
)

add_executable(
    02_validation_layers
    code/02_validation_layers.cpp
)

add_executable(
    03_physical_device_selection
    code/03_physical_device_selection.cpp
)

add_executable(
    04_logical_device
    code/04_logical_device.cpp
)

add_executable(
    05_window_surface
    code/05_window_surface.cpp
)

add_executable(
    06_swap_chain_creation
    code/06_swap_chain_creation.cpp
)

add_executable(
    07_image_views
    code/07_image_views.cpp
)

add_executable(
    08_graphics_pipeline
    code/08_graphics_pipeline.cpp
)

add_executable(
    09_shader_modules
    code/09_shader_modules.cpp
)

add_executable(
    10_fixed_functions
    code/10_fixed_functions.cpp
)

add_executable(
    11_render_passes
    code/11_render_passes.cpp
)

add_executable(
    12_graphics_pipeline_complete
    code/12_graphics_pipeline_complete.cpp
)

add_executable(
    13_framebuffers
    code/13_framebuffers.cpp
)

add_executable(
    14_command_buffers
    code/14_command_buffers.cpp
)

add_executable(
    15_hello_triangle
    code/15_hello_triangle.cpp
)

add_executable(
    16_swap_chain_recreation
    code/16_swap_chain_recreation.cpp
)

add_executable(
    17_vertex_input
    code/17_vertex_input.cpp
)

add_executable(
    18_vertex_buffer
    code/18_vertex_buffer.cpp
)

add_executable(
    19_staging_buffer
    code/19_staging_buffer.cpp
)

add_executable(
    20_index_buffer
    code/20_index_buffer.cpp
)

add_executable(
    21_descriptor_layout
    code/21_descriptor_layout.cpp
)

add_executable(
    22_descriptor_sets
    code/22_descriptor_sets.cpp
)

add_executable(
    23_texture_image
    code/23_texture_image.cpp
)

add_executable(
    24_sampler
    code/24_sampler.cpp
)

add_executable(
    25_texture_mapping
    code/25_texture_mapping.cpp
)

add_executable(
    26_depth_buffering
    code/26_depth_buffering.cpp
)

#add_executable(
#    27_model_loading
#    code/27_model_loading.cpp
#)

#add_executable(
#    28_mipmapping
#    code/28_mipmapping.cpp
#)

#add_executable(
#    29_multisampling
#    code/29_multisampling.cpp
#)


set(demo_shaders
        ./code/09_shader_base.frag
        ./code/09_shader_base.vert
        ./code/17_shader_vertexbuffer.frag
        ./code/17_shader_vertexbuffer.vert
        ./code/21_shader_ubo.frag
        ./code/21_shader_ubo.vert
        ./code/25_shader_textures.frag
        ./code/25_shader_textures.vert
        ./code/26_shader_depth.frag
        ./code/26_shader_depth.vert
)


find_package(Vulkan REQUIRED)
add_dependencies(00_base_code Vulkan::Vulkan)
add_dependencies(01_instance_creation Vulkan::Vulkan)
add_dependencies(02_validation_layers Vulkan::Vulkan)
add_dependencies(03_physical_device_selection Vulkan::Vulkan)
add_dependencies(04_logical_device Vulkan::Vulkan)
add_dependencies(05_window_surface Vulkan::Vulkan)
add_dependencies(06_swap_chain_creation Vulkan::Vulkan)
add_dependencies(07_image_views Vulkan::Vulkan)
add_dependencies(08_graphics_pipeline Vulkan::Vulkan)
add_dependencies(09_shader_modules Vulkan::Vulkan)
add_dependencies(10_fixed_functions Vulkan::Vulkan)
add_dependencies(11_render_passes Vulkan::Vulkan)
add_dependencies(12_graphics_pipeline_complete Vulkan::Vulkan)
add_dependencies(13_framebuffers Vulkan::Vulkan)
add_dependencies(14_command_buffers Vulkan::Vulkan)
add_dependencies(15_hello_triangle Vulkan::Vulkan)
add_dependencies(16_swap_chain_recreation Vulkan::Vulkan)
add_dependencies(17_vertex_input Vulkan::Vulkan)
add_dependencies(18_vertex_buffer Vulkan::Vulkan)
add_dependencies(19_staging_buffer Vulkan::Vulkan)
add_dependencies(20_index_buffer Vulkan::Vulkan)
add_dependencies(21_descriptor_layout Vulkan::Vulkan)
add_dependencies(22_descriptor_sets Vulkan::Vulkan)
add_dependencies(23_texture_image Vulkan::Vulkan)
add_dependencies(24_sampler Vulkan::Vulkan)
add_dependencies(25_texture_mapping Vulkan::Vulkan)
add_dependencies(26_depth_buffering Vulkan::Vulkan)
#add_dependencies(27_model_loading Vulkan::Vulkan)
#add_dependencies(28_mipmapping Vulkan::Vulkan)
#add_dependencies(29_multisampling Vulkan::Vulkan)
set(VULKAN_LIBRARIES "Vulkan::Vulkan")

# using PkgConfig to determine how to link against
# the system's glfw and curl
find_package(PkgConfig REQUIRED)
pkg_check_modules(GLFW REQUIRED glfw3)

include_directories(${GLFW_INCLUDE_DIR} ${Vulkan_INCLUDE_DIR} deps/stb/)


target_link_libraries(00_base_code dl m pthread
  ${GLFW_LIBRARIES} ${VULKAN_LIBRARIES})
target_link_libraries(01_instance_creation dl m pthread
  ${GLFW_LIBRARIES} ${VULKAN_LIBRARIES})
target_link_libraries(02_validation_layers dl m pthread
  ${GLFW_LIBRARIES} ${VULKAN_LIBRARIES})
target_link_libraries(03_physical_device_selection dl m pthread
  ${GLFW_LIBRARIES} ${VULKAN_LIBRARIES})
target_link_libraries(04_logical_device dl m pthread
  ${GLFW_LIBRARIES} ${VULKAN_LIBRARIES})
target_link_libraries(05_window_surface dl m pthread
  ${GLFW_LIBRARIES} ${VULKAN_LIBRARIES})
target_link_libraries(06_swap_chain_creation dl m pthread
  ${GLFW_LIBRARIES} ${VULKAN_LIBRARIES})
target_link_libraries(07_image_views dl m pthread
  ${GLFW_LIBRARIES} ${VULKAN_LIBRARIES})
target_link_libraries(08_graphics_pipeline dl m pthread
  ${GLFW_LIBRARIES} ${VULKAN_LIBRARIES})
target_link_libraries(09_shader_modules dl m pthread
  ${GLFW_LIBRARIES} ${VULKAN_LIBRARIES})
target_link_libraries(10_fixed_functions dl m pthread
  ${GLFW_LIBRARIES} ${VULKAN_LIBRARIES})
target_link_libraries(11_render_passes dl m pthread
  ${GLFW_LIBRARIES} ${VULKAN_LIBRARIES})
target_link_libraries(12_graphics_pipeline_complete dl m pthread
  ${GLFW_LIBRARIES} ${VULKAN_LIBRARIES})
target_link_libraries(13_framebuffers dl m pthread
  ${GLFW_LIBRARIES} ${VULKAN_LIBRARIES})
target_link_libraries(14_command_buffers dl m pthread
  ${GLFW_LIBRARIES} ${VULKAN_LIBRARIES})
target_link_libraries(15_hello_triangle dl m pthread
  ${GLFW_LIBRARIES} ${VULKAN_LIBRARIES})
target_link_libraries(16_swap_chain_recreation dl m pthread
  ${GLFW_LIBRARIES} ${VULKAN_LIBRARIES})
target_link_libraries(17_vertex_input dl m pthread
  ${GLFW_LIBRARIES} ${VULKAN_LIBRARIES})
target_link_libraries(18_vertex_buffer dl m pthread
  ${GLFW_LIBRARIES} ${VULKAN_LIBRARIES})
target_link_libraries(19_staging_buffer dl m pthread
  ${GLFW_LIBRARIES} ${VULKAN_LIBRARIES})
target_link_libraries(20_index_buffer dl m pthread
  ${GLFW_LIBRARIES} ${VULKAN_LIBRARIES})
target_link_libraries(21_descriptor_layout dl m pthread
  ${GLFW_LIBRARIES} ${VULKAN_LIBRARIES})
target_link_libraries(22_descriptor_sets dl m pthread
  ${GLFW_LIBRARIES} ${VULKAN_LIBRARIES})
target_link_libraries(23_texture_image dl m pthread
  ${GLFW_LIBRARIES} ${VULKAN_LIBRARIES})
target_link_libraries(24_sampler dl m pthread
  ${GLFW_LIBRARIES} ${VULKAN_LIBRARIES})
target_link_libraries(25_texture_mapping dl m pthread
  ${GLFW_LIBRARIES} ${VULKAN_LIBRARIES})
target_link_libraries(26_depth_buffering dl m pthread
  ${GLFW_LIBRARIES} ${VULKAN_LIBRARIES})
#target_link_libraries(27_model_loading dl m pthread
#  ${GLFW_LIBRARIES} ${VULKAN_LIBRARIES})
#target_link_libraries(28_mipmapping dl m pthread
#  ${GLFW_LIBRARIES} ${VULKAN_LIBRARIES})
#target_link_libraries(29_multisampling dl m pthread
#  ${GLFW_LIBRARIES} ${VULKAN_LIBRARIES})


set(SHADERS_DIR "${CMAKE_SOURCE_DIR}/code/")
set(OUTPUT_COPY_DIR ${CMAKE_CURRENT_BINARY_DIR})


add_custom_command(TARGET 00_base_code PRE_BUILD
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
    configure_file(./code/CompileShaders.sh.in ${CMAKE_BINARY_DIR}/CompileShaders.sh @ONLY)

    add_custom_command(TARGET 00_base_code POST_BUILD DEPENDS ${demo_shaders}
        COMMAND ${CMAKE_BINARY_DIR}/CompileShaders.sh
        )
endif()



# Install
install(TARGETS 00_base_code DESTINATION bin)
install(TARGETS 01_instance_creation DESTINATION bin)
install(TARGETS 02_validation_layers DESTINATION bin)
install(TARGETS 03_physical_device_selection DESTINATION bin)
install(TARGETS 04_logical_device DESTINATION bin)
install(TARGETS 05_window_surface DESTINATION bin)
install(TARGETS 06_swap_chain_creation DESTINATION bin)
install(TARGETS 07_image_views DESTINATION bin)
install(TARGETS 08_graphics_pipeline DESTINATION bin)
install(TARGETS 09_shader_modules DESTINATION bin)
install(TARGETS 10_fixed_functions DESTINATION bin)
install(TARGETS 11_render_passes DESTINATION bin)
install(TARGETS 12_graphics_pipeline_complete DESTINATION bin)
install(TARGETS 13_framebuffers DESTINATION bin)
install(TARGETS 14_command_buffers DESTINATION bin)
install(TARGETS 15_hello_triangle DESTINATION bin)
install(TARGETS 16_swap_chain_recreation DESTINATION bin)
install(TARGETS 17_vertex_input DESTINATION bin)
install(TARGETS 18_vertex_buffer DESTINATION bin)
install(TARGETS 19_staging_buffer DESTINATION bin)
install(TARGETS 20_index_buffer DESTINATION bin)
install(TARGETS 21_descriptor_layout DESTINATION bin)
install(TARGETS 22_descriptor_sets DESTINATION bin)
install(TARGETS 23_texture_image DESTINATION bin)
install(TARGETS 24_sampler DESTINATION bin)
install(TARGETS 25_texture_mapping DESTINATION bin)
install(TARGETS 26_depth_buffering DESTINATION bin)
#install(TARGETS 27_model_loading DESTINATION bin)
#install(TARGETS 28_mipmapping DESTINATION bin)
#install(TARGETS 29_multisampling DESTINATION bin)

install(DIRECTORY ${CMAKE_BINARY_DIR}/shaders/ DESTINATION shaders/)
install(DIRECTORY resources/ DESTINATION resources/)
