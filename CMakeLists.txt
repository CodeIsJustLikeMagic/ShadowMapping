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
    ${MY_PROJECT_INCLUDE_DIR}/glfw-3.1.2/include

)
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/")
# OpenGL
find_package(OpenGL REQUIRED)
# GLM
find_package(GLM REQUIRED)
message(STATUS "GLM included at ${GLM_INCLUDE_DIR}")

# STB_IMAGE
add_library(STB_IMAGE "thirdparty/stb_image.cpp")

# GLAD
add_library(GLAD "thirdparty/glad.c")

set(LIBS opengl32 STB_IMAGE GLAD)

#set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 ")


ADD_EXECUTABLE(${PROJECT_NAME}
    
    ${MY_SOURCE_FILES}

 )
TARGET_LINK_LIBRARIES(${PROJECT_NAME}

    glfw ${GLFW_LIBRARIES}
    ${LIBS}

)
