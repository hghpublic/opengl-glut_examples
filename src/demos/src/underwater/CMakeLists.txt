cmake_minimum_required(VERSION 4.1)

project(underwater C)

find_package(OpenGL REQUIRED)
find_package(FreeGLUT CONFIG REQUIRED)
find_package(GLUT REQUIRED)


set(target underwater)
add_executable(${target})
target_compile_features(${target} PRIVATE c_std_23)
target_link_libraries(${target} PRIVATE OpenGL::GL OpenGL::GLU)
target_link_libraries(${target} PRIVATE
    $<IF:$<TARGET_EXISTS:FreeGLUT::freeglut>,
        FreeGLUT::freeglut,
        FreeGLUT::freeglut_static>)
target_link_libraries(${target} PRIVATE GLUT::GLUT)

target_sources(${target} PRIVATE
    underwater.c
    
    dino.c
    texload.c
)


# copy resources

set(resources
    caust00.bw
    caust01.bw
    caust02.bw
    caust03.bw
    caust04.bw
    caust05.bw
    caust06.bw
    caust07.bw
    caust08.bw
    caust09.bw
    caust10.bw
    caust11.bw
    caust12.bw
    caust13.bw
    caust14.bw
    caust15.bw
    caust16.bw
    caust17.bw
    caust18.bw
    caust19.bw
    caust20.bw
    caust21.bw
    caust22.bw
    caust23.bw
    caust24.bw
    caust25.bw
    caust26.bw
    caust27.bw
    caust28.bw
    caust29.bw
    caust30.bw
    caust31.bw

    floor.rgb
)

foreach(res ${resources})
add_custom_command(TARGET ${target} PRE_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy
    ${CMAKE_CURRENT_SOURCE_DIR}/${res}
    $<TARGET_FILE_DIR:${target}>/
)    
endforeach()
