cmake_minimum_required(VERSION 2.6)

project(kaze_demo)

find_package(OpenCV 2.4.9 REQUIRED)

set(CMAKE_CXX_FLAGS " -msse -msse2 -msse3 -mfpmath=sse")

find_package(OpenMP)
if (OPENMP_FOUND)
    set (CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${OpenMP_C_FLAGS}")
    set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${OpenMP_CXX_FLAGS}")
endif()

set(KAZE_SRC KAZE/kaze_config.cpp             
             KAZE/kaze_ipoint.cpp
             KAZE/kaze_nldiffusion_functions.cpp
             KAZE/kaze_utils.cpp
             KAZE/kaze.cpp
             KAZE/kaze_features.cpp
)

include_directories(${OpenCV_INCLUDE_DIRS})

add_executable(kaze_demo KazeOpenCV.cpp ${KAZE_SRC})

target_link_libraries(kaze_demo ${OpenCV_LIBS})
