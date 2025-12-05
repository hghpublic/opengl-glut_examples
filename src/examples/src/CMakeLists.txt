# cmake_minimum_required(VERSION 4.1)

# project(examples C)

find_package(OpenGL REQUIRED)
find_package(FreeGLUT CONFIG REQUIRED)
find_package(GLUT REQUIRED)


# targets

set(targets
    abgr
    bitfont
    blender
    cube
    dials
    dials2
    dinoball
    dinoshade
    dinospin
    evaltest
    fogtst
    fontdemo
    glpuzzle
    glutdino
    glutplane
    halomagic
    highlight
    lightlab
    mjksift
    mjkwarp
    molehill
    movelight
    oclip
    ohidden
    olight
    olympic
    origami
    oversphere
    reflectdino
    rendereps
    sb2db
    scene
    screendoor
    scube
    simple
    sphere
    sphere2
    splatlogo
    spots
    stars
    stenciltst
    stereo
    stroke
    subwin
    surfgrid
    texenv
    ## trackball
    trippy
    triselect
    zoomdino
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


# targets with logo dependency

target_sources(splatlogo PRIVATE
    logo.c
)

# targets with mjkimage dependency

foreach(target mjksift; mjkwarp)
target_sources(${target} PRIVATE
    mjkimage.c
)
endforeach()

# targets with trackball dependency

foreach(target dinospin; glpuzzle)
target_sources(${target} PRIVATE
    trackball.c
)
endforeach()
