cmake_minimum_required(VERSION 3.22)
#set(CMAKE_C 17)
set(CMAKE_OSX_ARCHITECTURES x86_64)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY /usr/local/lib)

project(glyphme)
#---------------------------
include_directories(/usr/local/include)
include_directories(c_src)

add_library(glyphme SHARED c_src/glyphme.cpp c_src/stb_truetype.h)

#LIBHL
find_library(LIBHL NAMES hl HINTS /usr/local/lib)
target_link_libraries(glyphme ${LIBHL})

#OUTPUT
set_target_properties(
        glyphme
        PROPERTIES
        RUNTIME_OUTPUT_DIRECTORY ${CMAKE_LIBRARY_OUTPUT_DIRECTORY}
        LIBRARY_OUTPUT_DIRECTORY ${CMAKE_LIBRARY_OUTPUT_DIRECTORY}
        OUTPUT_NAME "glyphme"
        SUFFIX .hdll
        PREFIX ""
)

install(TARGETS glyphme)