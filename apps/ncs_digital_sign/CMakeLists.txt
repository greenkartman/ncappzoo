project(ncs_digital_sign)
cmake_minimum_required(VERSION 2.8)

include_directories(
	$ENV{INTEL_OPENVINO_DIR}/opencv/include
	
)

set(SOURCES
    cpp/run.cpp
)

        
add_executable(ncs_digital_sign ${SOURCES})

find_package(InferenceEngine)
include_directories(${InferenceEngine_INCLUDE_DIRS})
find_library(OPENCV_CORE opencv_core HINTS $ENV{INTEL_CVSDK_DIR}/opencv/lib)
find_library(OPENCV_HIGHGUI opencv_highgui HINTS $ENV{INTEL_CVSDK_DIR}/opencv/lib)
find_library(OPENCV_IMGPROC opencv_imgproc HINTS $ENV{INTEL_CVSDK_DIR}/opencv/lib)
find_library(OPENCV_CODECS opencv_imgcodecs HINTS $ENV{INTEL_CVSDK_DIR}/opencv/lib)
find_library(OPENCV_VIDEOIO opencv_videoio HINTS $ENV{INTEL_CVSDK_DIR}/opencv/lib)

target_link_libraries(ncs_digital_sign ${InferenceEngine_LIBRARIES} dl ${OPENCV_CORE} ${OPENCV_HIGHGUI} ${OPENCV_IMGPROC} ${OPENCV_CODECS} ${OPENCV_VIDEOIO})

set(CMAKE_CXX_FLAGS "-Wall -std=c++11")