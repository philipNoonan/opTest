cmake_minimum_required(VERSION 2.8.7)

### FIND VCPKG
if(DEFINED ENV{VCPKG_ROOT} AND NOT DEFINED CMAKE_TOOLCHAIN_FILE)
  set(CMAKE_TOOLCHAIN_FILE "$ENV{VCPKG_ROOT}/scripts/buildsystems/vcpkg.cmake"
      CACHE STRING "")
endif()

project(opTest)

add_definitions(-std=c++11)



find_package(openpose REQUIRED)
find_package(OpenCV REQUIRED)
find_package(Caffe REQUIRED)
find_package(glog REQUIRED)
find_package(protobuf REQUIRED)
find_package(hdf5 REQUIRED)
find_package(gflags REQUIRED)
find_package(OpenGL REQUIRED)
find_package(GLEW REQUIRED)
find_package(glfw3 REQUIRED)
find_package(glm REQUIRED)
find_package(imgui REQUIRED)

file(GLOB_RECURSE SRC "src/*")
file(GLOB_RECURSE GFX "graphics/*")

list(APPEND SRC ${GFX})

add_executable(${PROJECT_NAME} ${SRC})

target_include_directories(${PROJECT_NAME} PUBLIC 
	${OpenCV_INCLUDE_DIRS}
	${OpenPose_INCLUDE_DIRS}
	${GFLAGS_INCLUDE_DIR}
	${GLOG_INCLUDE_DIR}
	"graphics"
	)



target_link_libraries(${PROJECT_NAME} 
      ${OpenCV_LIBS}
	  ${OPENGL_gl_LIBRARY}
	  OpenPose::openpose
	  protobuf::libprotobuf
	  hdf5::hdf5-shared
	  gflags
	  glog::glog
	  caffe
	  GLEW::GLEW
	  glfw
	  glm
	  imgui::imgui)
