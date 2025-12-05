cmake_minimum_required(VERSION 4.1)

project(yacme C)

find_package(OpenGL REQUIRED)
find_package(FreeGLUT CONFIG REQUIRED)
find_package(GLUT REQUIRED)


set(target yacme)
add_executable(${target})
target_compile_features(${target} PRIVATE c_std_23)
target_compile_definitions(${target} PRIVATE YACME_DBG)
target_link_libraries(${target} PRIVATE OpenGL::GL OpenGL::GLU)
target_link_libraries(${target} PRIVATE
    $<IF:$<TARGET_EXISTS:FreeGLUT::freeglut>,
        FreeGLUT::freeglut,
        FreeGLUT::freeglut_static>)
target_link_libraries(${target} PRIVATE GLUT::GLUT)

target_sources(${target} PRIVATE
    Editor.c
    invertmat.c
)
