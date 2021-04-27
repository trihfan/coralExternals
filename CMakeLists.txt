cmake_minimum_required(VERSION 3.16)

# Project
set(version "1.0.0")
project(coralExternals VERSION ${version} LANGUAGES CXX)
set_property(GLOBAL PROPERTY USE_FOLDERS ON)

# Set c++17
set(CMAKE_CXX_STANDARD 17)
if(UNIX AND NOT APPLE)
        set(CMAKE_CXX_LINK_FLAGS "${CMAKE_CXX_LINK_FLAGS} -lstdc++ -std=c++17")
endif()

# define output directories
set(lib_output_directory ${PROJECT_BINARY_DIR}/lib)
set(bin_output_directory ${PROJECT_BINARY_DIR}/bin)

# Emscripten config
if(EMSCRIPTEN)
    add_compile_options("-s" "USE_FREETYPE=1")
    set(CMAKE_CXX_LINK_FLAGS "${CMAKE_CXX_LINK_FLAGS} -s USE_GLFW=3 -s USE_WEBGL2=1 -s FULL_ES3=1 -s WASM=1 -s USE_FREETYPE=1 --preload-file ${bin_output_directory}/assets@/assets")
endif()

# subdirectories
add_subdirectory(externals) # Properties: glm_path, assimp_path
