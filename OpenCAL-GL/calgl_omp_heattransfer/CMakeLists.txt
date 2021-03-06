cmake_minimum_required(VERSION 2.8 FATAL_ERROR)

find_package(OpenCAL 1.1 COMPONENTS  OpenCAL-OMP OpenCAL-GL REQUIRED)
find_package(Threads REQUIRED)
find_package(OpenGL  REQUIRED)
find_package(GLUT REQUIRED)

if(NOT MSVC)
  find_library(M_LIB m)
else()
  # not needed on windows
  set(M_LIB "")
endif()

include_directories(
	${CMAKE_CURRENT_SOURCE_DIR}/include
	${OPENGL_INCLUDE_DIRS}
	${GLUT_INCLUDE_DIR}
	${OPENCAL_INCLUDE_DIR}
)

link_directories(${CMAKE_CURRENT_SOURCE_DIR}/source)

file(GLOB SRC
    "include/*.h"
    "source/*.cpp"
    "source/*.c"
)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/bin)

add_executable(calgl_omp_heat ${SRC})
target_link_libraries(calgl_omp_heat ${OPENCAL_LIBRARIES} ${M_LIB} ${OPENGL_LIBRARIES} ${GLUT_glut_LIBRARY} pthread)
