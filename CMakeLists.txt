cmake_minimum_required(VERSION 2.8.7)
project(DeepMAR_deploy)

enable_testing()

set(TEST ON CACHE BOOL "Whether to use CPU onlu.")
set(CPU_ONLY OFF CACHE BOOL "Whether to use CPU onlu.")
set(CAFFE_HOME $ENV{CAFFE_HOME} CACHE PATH "Home directory of Caffe.")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -fopenmp")
set(JAVA_HOME $ENV{JAVA_HOME} CACHE PATH "Home directory of Java Divelooment Toolkit (JDK).")

add_subdirectory(src lib)

add_subdirectory(jni lib/jni)

set(TEST_IMG_PATH CACHE FILEPATH "File path of image for test.")
add_subdirectory(test bin)

install(FILES
        ${PROJECT_SOURCE_DIR}/lib/libDeepMAR.so
        ${PROJECT_SOURCE_DIR}/lib/jni/libDeepMARCaffeNative.so
        DESTINATION
        lib)