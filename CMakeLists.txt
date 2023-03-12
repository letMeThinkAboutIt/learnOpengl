cmake_minimum_required(VERSION 3.20)

project(learnOpengl LANGUAGES C CXX)

#thirdPartyLib
set(thirdPartyLibPath "./thirdPartyLib")

#glad
set(GLAD_DIR "${thirdPartyLibPath}/glad")
#message("include_dir = ${INCLUDE_DIR}")
list(APPEND LOCAL_INCLUDE_DIR "${GLAD_DIR}/include")

#glfw]
set(GLFW_DIR "${thirdPartyLibPath}/glfw-3.3.8")

option(GLFW_BUILD_EXAMPLES "Build the GLFW example programs" OFF)
option(GLFW_BUILD_TESTS "Build the GLFW test programs" OFF)
option(GLFW_BUILD_DOCS "Build the GLFW documentation" OFF)
option(GLFW_INSTALL "Generate installation target" OFF)

add_subdirectory(${GLFW_DIR} glfw_binary EXCLUDE_FROM_ALL)
list(APPEND LOCAL_INCLUDE_DIR "${GLFW_DIR}/include")
list(APPEND LOCAL_INCLUDE_DIR "${GLFW_DIR}/deps")

list(APPEND LINK_LIBS glfw)

list(APPEND srcCode 
        "${GLAD_DIR}/src/glad.c"
        "./src/main.cpp")

add_executable(openglApp ${srcCode})

target_include_directories(openglApp PUBLIC ${LOCAL_INCLUDE_DIR})
target_link_libraries(openglApp PUBLIC ${LINK_LIBS} )

