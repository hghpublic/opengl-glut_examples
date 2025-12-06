
find_package(OpenGL REQUIRED)
find_package(FreeGLUT CONFIG REQUIRED)
find_package(GLUT REQUIRED)

set(target mui)
add_library(${target})
target_compile_features(${target} PRIVATE c_std_23)
target_include_directories(${target} PRIVATE ${PROJECT_SOURCE_DIR}/include)
target_include_directories(${target} PUBLIC INTERFACE ${PROJECT_SOURCE_DIR}/include)
target_link_libraries(${target} PRIVATE OpenGL::GL OpenGL::GLU)
target_link_libraries(${target} PRIVATE
    $<IF:$<TARGET_EXISTS:FreeGLUT::freeglut>,
        FreeGLUT::freeglut,
        FreeGLUT::freeglut_static>)
target_link_libraries(${target} PRIVATE GLUT::GLUT)
target_sources(${target} PRIVATE
    browseparse.c
    browser.c
    button.c
    displaylist.c
    gizmo.c
    glutmui.c
    hslider.c
    miscui.c
    mui.c
    pulldown.c
    textlist.c
    uicolor.c
    vslider.c
)
