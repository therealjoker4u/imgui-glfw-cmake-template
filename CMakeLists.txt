cmake_minimum_required(VERSION 3.0.0)
project(app VERSION 0.1.0)

include(CTest)
enable_testing()

find_package(OpenGL REQUIRED)

# use STATIC instead of SHARED if you want to attach imgui library to your executable file.
add_library(imgui SHARED lib/imgui/imgui.cpp lib/imgui/imgui_demo.cpp lib/imgui/imgui_draw.cpp lib/imgui/imgui_tables.cpp lib/imgui/imgui_widgets.cpp)

add_executable(${PROJECT_NAME} src/main.cpp src/implementions/imgui_impl_glfw.cpp src/implementions/imgui_impl_opengl3.cpp)

set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})

target_include_directories(${PROJECT_NAME} PUBLIC $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>/lib)

set(GLFW3_LIB ${PROJECT_SOURCE_DIR}/lib/glfw/glfw3dll.lib)

target_link_libraries(${PROJECT_NAME} PUBLIC imgui ${GLFW3_LIB} opengl32)

include(CPack)