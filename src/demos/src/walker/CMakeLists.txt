cmake_minimum_required(VERSION 4.1)

project(walker C)

find_package(OpenGL REQUIRED)
find_package(FreeGLUT CONFIG REQUIRED)
find_package(GLUT REQUIRED)


set(target walker)
add_executable(${target})
target_compile_features(${target} PRIVATE c_std_23)
target_link_libraries(${target} PRIVATE OpenGL::GL OpenGL::GLU)
target_link_libraries(${target} PRIVATE
    $<IF:$<TARGET_EXISTS:FreeGLUT::freeglut>,
        FreeGLUT::freeglut,
        FreeGLUT::freeglut_static>)
target_link_libraries(${target} PRIVATE GLUT::GLUT)

target_sources(${target} PRIVATE
    walker.c
    
    models.c
    walkviewer.c
)


# copy resources

set(resources
    bound.cset
    dunk.cset
    Impossible.cset
    kick.cset
    moonwalk.cset
    MrFlex.cset
    newcurve0.cset
    Ouch.cset
    reverse_dunk.cset
    running.cset
    walk_backwards.cset
    walking.cset
)

foreach(res ${resources})
add_custom_command(TARGET ${target} PRE_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy
    ${CMAKE_CURRENT_SOURCE_DIR}/${res}
    $<TARGET_FILE_DIR:${target}>/
)    
endforeach()
