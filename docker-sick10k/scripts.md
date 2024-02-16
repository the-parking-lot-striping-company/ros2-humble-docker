Command to launch docker compose 

docker commands need be run from the directory this txt file is located which is "docker-sick10k"

```
docker compose -f docker-compose.yml up -d 
```
if you don't want detached mode for docker run 
```
docker compose if docker-compose.yml up 
```

The next step will allow you to open a terminal linked with a docker
```
docker exec -it docker-sick10k-realsense_ros2-1 bash
```
every time you open a new terminal run as you will be in ros_ws in docker
```
source install/setup.bash
```
command to run the lidar - do note certain network configurations need to be made
```
source install/setup.bash
ros2 launch sick_scan_xd sick_multiscan.launch.py
```

open new terminal and run the realsense with
```
source install/setup.bash
ros2 launch realsense2_camera rs_launch.py pointcloud.enable:=true
```

open new terminal and start foxglove bridge
```
source install/setup.bash
ros2 launch foxglove_bridge foxglove_bridge_launch.xml
```

