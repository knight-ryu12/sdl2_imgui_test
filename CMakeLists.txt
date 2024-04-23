cmake_minimum_required(VERSION 3.11)
project(sdl2_vulkan)

include(ExternalProject)
include(FetchContent)

add_subdirectory(3rdparty/SDL)
add_subdirectory(3rdparty/SDL-Mixer-X)

FetchContent_Declare(
    imgui
    GIT_REPOSITORY https://github.com/ocornut/imgui.git
    GIT_TAG master
)

FetchContent_MakeAvailable(imgui)
set(IMGUI_DIR ${imgui_SOURCE_DIR})

add_executable(sdl2_vulkan main.cpp 
	
${IMGUI_DIR}/imgui.cpp
${IMGUI_DIR}/imgui_draw.cpp
${IMGUI_DIR}/imgui_tables.cpp
${IMGUI_DIR}/imgui_widgets.cpp
${IMGUI_DIR}/imgui_demo.cpp

${IMGUI_DIR}/backends/imgui_impl_sdl2.cpp
#${IMGUI_DIR}/backends/imgui_impl_sdl3.cpp
${IMGUI_DIR}/backends/imgui_impl_sdlrenderer2.cpp
)

#add_dependencies(sdl2_vulkan sdl2_project)

target_include_directories(sdl2_vulkan PRIVATE include ${IMGUI_DIR} ${IMGUI_DIR}/backends)

target_link_libraries(sdl2_vulkan SDL2::SDL2main SDL2::SDL2-static)