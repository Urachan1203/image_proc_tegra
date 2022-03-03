cmake_minimum_required(VERSION 3.5)
project(image_proc_tegra)

find_package(OpenCV REQUIRED)

if(CUDA_FOUND)
message("--------")
message("CUDA Found")
endif()

find_package(catkin REQUIRED COMPONENTS
  cv_bridge
  image_transport
  image_geometry
  sensor_msgs
  std_msgs
  roscpp
  nodelet  
)

catkin_package(
  CATKIN_DEPENDS image_geometry roscpp sensor_msgs
  LIBRARIES ${PROJECT_NAME}
)

include_directories(SYSTEM ${catkin_INCLUDE_DIRS} ${OpenCV_INCLUDE_DIRS})

add_library(${PROJECT_NAME}     src/nodelets/rectify.cpp )
target_link_libraries(${PROJECT_NAME} ${catkin_LIBRARIES} ${OpenCV_LIBRARIES})

add_executable(image_proc_tegra_exe src/image_proc_tegra.cpp)

target_link_libraries(image_proc_tegra_exe
   ${PROJECT_NAME}
   ${catkin_LIBRARIES}
)
