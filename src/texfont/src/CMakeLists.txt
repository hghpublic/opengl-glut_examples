

# targets

set(targets
    gentexfont
    showtxf
    simpletxf
    txfdemo
)

foreach(target ${targets})
add_executable(${target})
target_link_libraries(${target} PRIVATE OpenGL::GL OpenGL::GLU)
target_link_libraries(${target} PRIVATE
    $<IF:$<TARGET_EXISTS:FreeGLUT::freeglut>,
        FreeGLUT::freeglut,
        FreeGLUT::freeglut_static>)
target_link_libraries(${target} PRIVATE GLUT::GLUT)
endforeach(target)


# target sources

target_sources(gentexfont PRIVATE
    gentexfont.c
    texfont.c
)


target_sources(showtxf PRIVATE
    showtxf.c
    texfont.c
)

target_sources(simpletxf PRIVATE
    simpletxf.c
    texfont.c
)

target_sources(txfdemo PRIVATE
    txfdemo.c
    texfont.c
)


# copy resources

set(resources
    curlfont.txf
    default.txf
    djb.txf
    haeberli.txf
    rockfont.txf
    sorority.txf
)
set(target txfdemo)
foreach(res ${resources})
add_custom_command(TARGET ${target} PRE_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy
    ${CMAKE_CURRENT_SOURCE_DIR}/${res}
    $<TARGET_FILE_DIR:${target}>/
)    
endforeach()
