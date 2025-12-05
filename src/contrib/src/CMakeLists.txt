# cmake_minimum_required(VERSION 4.1)

# project(contrib C)

find_package(OpenGL REQUIRED)
find_package(FreeGLUT CONFIG REQUIRED)
find_package(GLUT REQUIRED)


# targets

set(targets
    agv_example
    # engine
    # fractals
    gears
    hanoi
    # hanoi2
    lineblend
    moth
    noof
    rings
    steam
    text3d
    worms
)


foreach(target ${targets})
add_executable(${target})
target_compile_features(${target} PRIVATE c_std_23)
target_link_libraries(${target} PRIVATE OpenGL::GL OpenGL::GLU)
target_link_libraries(${target} PRIVATE
    $<IF:$<TARGET_EXISTS:FreeGLUT::freeglut>,
        FreeGLUT::freeglut,
        FreeGLUT::freeglut_static>)
target_link_libraries(${target} PRIVATE GLUT::GLUT)
    
target_sources(${target} PRIVATE
    ${target}.c
)
endforeach()



# targets with agv dependency

target_sources(agv_example PRIVATE agviewer.c)


# target_compile_definitions(engine PRIVATE TEST_ENGINE)
