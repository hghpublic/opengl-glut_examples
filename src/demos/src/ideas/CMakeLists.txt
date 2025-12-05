cmake_minimum_required(VERSION 4.1)

project(ideas C)

find_package(OpenGL REQUIRED)
find_package(FreeGLUT CONFIG REQUIRED)
find_package(GLUT REQUIRED)


set(target ideas)
add_executable(${target})
target_compile_features(${target} PRIVATE c_std_23)
target_link_libraries(${target} PRIVATE OpenGL::GL OpenGL::GLU)
target_link_libraries(${target} PRIVATE
    $<IF:$<TARGET_EXISTS:FreeGLUT::freeglut>,
        FreeGLUT::freeglut,
        FreeGLUT::freeglut_static>)
target_link_libraries(${target} PRIVATE GLUT::GLUT)

target_sources(${target} PRIVATE
    track.c
    
    draw_holder.c
    draw_lamp.c
    draw_logo.c
    draw_logo_line.c
    draw_logo_shadow.c
    
    a.c
    b.c
    d.c
    e.c
    f.c
    h.c
    i.c
    m.c
    n.c
    o.c
    p.c
    r.c
    s.c
    t.c
    w.c
)
