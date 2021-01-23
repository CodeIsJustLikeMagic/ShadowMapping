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

SET(MY_SOURCE_FILES

    ${MY_PROJECT_SOURCE_DIR}/ShadowMapping.cpp
    
)
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/")
# OpenGL
find_package(OpenGL REQUIRED)
find_package(ASSIMP REQUIRED)
message(STATUS "Found ASSIMP in ${ASSIMP_INCLUDE_DIR}")
# Put all libraries into a variable
set(opengl32 assimp)
INCLUDE_DIRECTORIES(

    ${MY_PROJECT_INCLUDE_DIR}
    ${CMAKE_SOURCE_DIR}/src
	${CMAKE_SOURCE_DIR}/include

)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 ")

LINK_DIRECTORIES(

    ${CMAKE_SOURCE_DIR}/lib # add lib files

)


ADD_EXECUTABLE(${PROJECT_NAME}
    
    ${MY_SOURCE_FILES}

)
TARGET_LINK_LIBRARIES(${PROJECT_NAME}

    

)
