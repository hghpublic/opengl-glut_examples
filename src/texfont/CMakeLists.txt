cmake_minimum_required(VERSION 4.1)

project(texfont C)

find_package(OpenGL REQUIRED)
find_package(FreeGLUT CONFIG REQUIRED)
find_package(GLUT REQUIRED)

add_subdirectory(src)
