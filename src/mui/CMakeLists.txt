cmake_minimum_required(VERSION 4.1)

project(mui C)

# add_subdirectory(markkilgard/glut)

include(FetchContent)
FetchContent_Declare(
  mui
  GIT_REPOSITORY https://github.com/hghpublic/opengl-glut_examples.git
  GIT_TAG        markkilgard/glut/mui/dev/cmake
)
FetchContent_MakeAvailable(mui)

add_subdirectory(src)
