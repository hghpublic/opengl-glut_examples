# cmake_minimum_required(VERSION 4.1)

# project(examples C)

find_package(OpenGL REQUIRED)
find_package(FreeGLUT CONFIG REQUIRED)
find_package(GLUT REQUIRED)


# targets

set(targets
    bounce
    gamma
    gears
    # isosurf
    # offset
    reflect
    spin
    tess_demo
    texobj
    trdemo
    # winpos
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


# targets with image dependency

target_sources(reflect PRIVATE
    image.c
)

# targets with tr dependency

target_sources(trdemo PRIVATE
    tr.c
)

# targets with mjkimage dependency

# foreach(target mjksift; mjkwarp)
# target_sources(${target} PRIVATE
#     mjkimage.c
# )
# endforeach()

# targets with trackball dependency

# foreach(target dinospin; glpuzzle)
# target_sources(${target} PRIVATE
#     trackball.c
# )
# endforeach()
