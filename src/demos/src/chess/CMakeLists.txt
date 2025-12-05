cmake_minimum_required(VERSION 4.1)

project(chess C)

find_package(OpenGL REQUIRED)
find_package(FreeGLUT CONFIG REQUIRED)
find_package(GLUT REQUIRED)


set(target chess)
add_executable(${target})
target_compile_features(${target} PRIVATE c_std_23)
target_link_libraries(${target} PRIVATE OpenGL::GL OpenGL::GLU)
target_link_libraries(${target} PRIVATE
    $<IF:$<TARGET_EXISTS:FreeGLUT::freeglut>,
        FreeGLUT::freeglut,
        FreeGLUT::freeglut_static>)
target_link_libraries(${target} PRIVATE GLUT::GLUT)

target_sources(${target} PRIVATE
    main.c

    animate.c
    chess.c
    pathplan.c
    texture.c
)

add_custom_command(TARGET ${target} PRE_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy
    ${CMAKE_CURRENT_SOURCE_DIR}/chess.inp
    $<TARGET_FILE_DIR:${target}>/
)    
