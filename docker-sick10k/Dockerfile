FROM ros:humble-perception

ENV WS_DIR="/ros2_ws"
WORKDIR ${WS_DIR}

SHELL ["/bin/bash", "-c"]

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update \
 && apt-get install -y \
    build-essential \
    cmake \
    git-all \
    software-properties-common \
 && rm -rf /var/lib/apt/lists/*

RUN apt-get update \
 && apt-get install -y \
    ros-${ROS_DISTRO}-librealsense2* \
    ros-${ROS_DISTRO}-realsense2-* \
 && rm -rf /var/lib/apt/lists/*

RUN apt-get update \
 && apt-get install -y \
    ros-${ROS_DISTRO}-rviz2 \
 && rm -rf /var/lib/apt/lists/*

RUN apt-get update \
 && apt-get install -y \
    ros-${ROS_DISTRO}-foxglove-bridge \
    ros-${ROS_DISTRO}-diagnostic-updater \
    ros-${ROS_DISTRO}-diagnostic-msgs \
 && rm -rf /var/lib/apt/lists/*

RUN mkdir -p ${WS_DIR}/src \
 && cd ${WS_DIR}/src \
 && git clone https://github.com/SICKAG/sick_scan_xd.git \
 && git clone https://github.com/SICKAG/libsick_ldmrs.git

RUN source /opt/ros/humble/setup.bash \
   && cd ${WS_DIR} \
   && colcon build --packages-select libsick_ldmrs --event-handlers console_direct+ \
   && source ./install/setup.bash \
   && colcon build --packages-select sick_scan_xd --cmake-args " -DROS_VERSION=2" --event-handlers console_direct+ \
   && source ./install/setup.bash

ARG DEBIAN_FRONTEND=dialog
