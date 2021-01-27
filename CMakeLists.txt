# CMakeList.txt : Top-level CMake project file, do global configuration
# and include sub-projects here.
#
cmake_minimum_required (VERSION 3.8)

project ("ShadowMapping")
MESSAGE(${PROJECT_NAME} " root directory: " ${PROJECT_SOURCE_DIR})


SET(MY_OUTPUT_DIR "${PROJECT_SOURCE_DIR}/build")
MESSAGE(${PROJECT_NAME} " output directory: " ${MY_OUTPUT_DIR})

SET(LIBRARY_OUTPUT_DIRECTORY ${MY_OUTPUT_DIR})
SET(LIBRARY_OUTPUT_PATH      ${MY_OUTPUT_DIR})
SET(RUNTIME_OUTPUT_DIRECTORY ${MY_OUTPUT_DIR})
SET(ARCHIVE_OUTPUT_DIRECTORY ${MY_OUTPUT_DIR})
SET(EXECUTABLE_OUTPUT_PATH   ${MY_OUTPUT_DIR})

SET(MY_PROJECT_INCLUDE_DIR include)
SET(MY_PROJECT_SOURCE_DIR src)

SET(MY_HEADER_FILES

    ${MY_PROJECT_INCLUDE_DIR}/ShadowMapping.hpp

)

add_subdirectory(${MY_PROJECT_INCLUDE_DIR}/glfw-3.1.2)

SET(MY_SOURCE_FILES

    ${MY_PROJECT_SOURCE_DIR}/ShadowMapping.cpp
    ${MY_PROJECT_SOURCE_DIR}/texture.cpp
    ${MY_PROJECT_SOURCE_DIR}/controls.cpp
    ${MY_PROJECT_SOURCE_DIR}/objloader.cpp
    ${MY_PROJECT_SOURCE_DIR}/shader.cpp
    ${MY_PROJECT_SOURCE_DIR}/vboindexer.cpp
    
)
INCLUDE_DIRECTORIES(

    ${MY_PROJECT_INCLUDE_DIR}
    ${CMAKE_SOURCE_DIR}/src
	${CMAKE_SOURCE_DIR}/include
    external/AntTweakBar-1.16/include/
	external/glfw-3.1.2/include/
	external/glm-0.9.7.1/
	external/assimp-3.0.1270/include/
	external/bullet-2.81-rev2613/src/

)
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/")
# OpenGL
find_package(OpenGL REQUIRED)
# GLM
find_package(GLM REQUIRED)
message(STATUS "GLM included at ${GLM_INCLUDE_DIR}")

find_package(ASSIMP REQUIRED)
message(STATUS "Found ASSIMP in ${ASSIMP_INCLUDE_DIR}")
# Put all libraries into a variable

# STB_IMAGE
add_library(STB_IMAGE "thirdparty/stb_image.cpp")

# GLAD
add_library(GLAD "thirdparty/glad.c")

set(LIBS opengl32 assimp STB_IMAGE GLAD)

#set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 ")

LINK_DIRECTORIES(

    ${CMAKE_SOURCE_DIR}/lib # add lib files

)


ADD_EXECUTABLE(${PROJECT_NAME}
    
    ${MY_SOURCE_FILES}

 )
TARGET_LINK_LIBRARIES(${PROJECT_NAME}

    glfw ${GLFW_LIBRARIES}
    ${LIBS}

)
