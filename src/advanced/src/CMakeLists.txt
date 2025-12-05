# cmake_minimum_required(VERSION 4.1)

# project(advanced C)

find_package(OpenGL REQUIRED)
find_package(FreeGLUT CONFIG REQUIRED)
find_package(GLUT REQUIRED)


# targets

set(targets
    accumaa
    af_depthcue
    af_teapots
    boundary
    comp
    convolve
    csg
    decal
    dissolve
    envmap
    envphong
    field
    genmipmap
    haloed
    hello2rts
    hiddenline
    imgproc
    mipmap_lines
    motionblur
    multilight
    # occlude
    projshadow
    projtex
    rasonly
    shadowfun
    shadowmap
    shadowvol
    silhouette
    softshadow
    tess
    textext
    textile
    textrim
    tvertex
    videoresize
    vox
    warp
    zcomposite
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

# targets with texture dependency

set(target_w_texture
    comp
    envmap
    genmipmap
    imgproc
    mipmap_lines
    projtex
    textile
    textrim
    warp
)
foreach(target ${target_w_texture})
target_sources(${target} PRIVATE
    texture.c
)
endforeach()

# targets with izoom dependency

target_sources(mipmap_lines PRIVATE
    izoom.c
)

# targets with addfog dependency

foreach(target af_depthcue; af_teapots)
target_sources(${target} PRIVATE
    addfog.c
)
endforeach()

# targets with rts dependency

target_sources(hello2rts PRIVATE
    rts.c
)

# targets with sphere dependency

foreach(target videoresize; tess)
target_sources(${target} PRIVATE
    sphere.c
)
endforeach()

# targets with textmap dependency

target_sources(textext PRIVATE
    textmap.c
    texture.c
)
