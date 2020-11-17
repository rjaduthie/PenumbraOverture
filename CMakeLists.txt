cmake_minimum_required (VERSION 2.6)
project(Overture)

add_subdirectory(../OALWrapper ../OALWrapper)
add_subdirectory(../hpl1engine ../hpl1engine)

include_directories(
    ${CMAKE_CURRENT_SOURCE_DIR}/../dependencies/include
        ${CMAKE_CURRENT_SOURCE_DIR}/../hpl1engine/include
    ${CMAKE_CURRENT_SOURCE_DIR}/../OALWrapper/include
)

link_directories(
    ${CMAKE_CURRENT_SOURCE_DIR}/../dependencies/lib/linux
)

#find_library(LIB_ANGELSCRIPT NAMES angelscript PATHS ../dependencies/lib/linux)
#add_library(angelscript STATIC IMPORTED)
#set_target_properties(angelscript PROPERTIES IMPORTED_LOCATION ${CMAKE_CURRENT_SOURCE_DIR}/../dependencies/lib/linux/libangelscript.a)

set(CMAKE_EXECUTABLE_SUFFIX .bin)

file(GLOB all_sources ${CMAKE_CURRENT_SOURCE_DIR}/*.cpp)

add_executable(Overture ${all_sources})

set_target_properties(Overture PROPERTIES
    INSTALL_RPATH_USE_LINK_PATH false
    OUTPUT_NAME overture)

target_link_libraries(Overture HPL OALWrapper Newton angelscript fltk GLEW GL GLU Cg CgGL ogg vorbis vorbisfile openal alut SDL SDL_ttf SDL_image)
