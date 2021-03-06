cmake_minimum_required(VERSION 3.1)

set(CMAKE_CXX_STANDARD 14)

find_package(OpenGL REQUIRED)
find_package(Freetype REQUIRED)

include_directories(${PROJECT_SOURCE_DIR}/include)

link_directories(${PROJECT_SOURCE_DIR}/lib)

option(GLFW_BUILD_DOCS OFF)
option(GLFW_BUILD_EXAMPLES OFF)
option(GLFW_BUILD_TESTS OFF)
add_subdirectory(glfw)

add_executable(Test src/Test.cpp src/glad.c)
target_link_libraries(Test glfw ${OPENGL_gl_LIBRARY})

add_executable(Water1 src/Water1.cpp src/Skybox.cpp src/Waves.cpp src/glad.c)
target_link_libraries(Water1 glfw ${OPENGL_gl_LIBRARY})

add_executable(Water2
        src/Water2.cpp
        src/Skybox.cpp
        src/VertexBufferOcean.cpp
        src/TextRenderer.cpp
        src/glad.c)
target_link_libraries(Water2 glfw ${OPENGL_gl_LIBRARY} ${FREETYPE_LIBRARIES}
        libbz2.dylib libz.dylib) # Things needed for Freetype on Mac OS X

add_executable(Ocean
        src/Water3.cpp
        src/Skybox.cpp
        src/Ocean.cpp
        src/TextRenderer.cpp
        src/glad.c)
target_link_libraries(Ocean glfw ${OPENGL_gl_LIBRARY} ${FREETYPE_LIBRARIES}
        libbz2.dylib libz.dylib) # Things needed for Freetype on Mac OS X

add_executable(FFTTest src/FFTTest.cpp)