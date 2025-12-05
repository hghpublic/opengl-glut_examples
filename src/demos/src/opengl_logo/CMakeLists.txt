cmake_minimum_required(VERSION 4.1)

project(opengl_logo C)

find_package(OpenGL REQUIRED)
find_package(FreeGLUT CONFIG REQUIRED)
find_package(GLUT REQUIRED)


set(target opengl_logo)
add_executable(${target})
target_compile_features(${target} PRIVATE c_std_23)
target_link_libraries(${target} PRIVATE OpenGL::GL OpenGL::GLU)
target_link_libraries(${target} PRIVATE
    $<IF:$<TARGET_EXISTS:FreeGLUT::freeglut>,
        FreeGLUT::freeglut,
        FreeGLUT::freeglut_static>)
target_link_libraries(${target} PRIVATE GLUT::GLUT)

target_sources(${target} PRIVATE
    opengl_logo.c
    def_logo.c
)
