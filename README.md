# tuw_uvc
## Dependencies
sudo apt-get install libv4l-dev
sudo apt-get install libsdl2-dev
## Create a costomized camera driver
```
roscd tuw_uvc
rosrun tuw_uvc update_dynamic_reconfigure -d /dev/video0 -f cfg/CameraXYZParameters.cfg
chmod u+x cfg/CameraXYZParameters.cfg
cp src/general_node.cpp src/camera_xyz_node.cpp
sed -i 's/CameraGeneralConfig/CameraXYZConfig/g' src/cameraXYZ15_node.cpp
sed -i 's/CameraParameters/CameraXYZ/g' cfg/CameraXYZParameters.cfg
```
Update the CMakeLists.txt and the the following statements
```
add_executable(camera_xyz_node src/camera_xyz_node.cpp)

...

target_link_libraries(camera_xyz_node tuw_uvc_ros 
  ${catkin_LIBRARIES}  ${OpenCV_LIBRARIES})
add_dependencies(camera_xyz_node tuw_uvc_ros) 
```



