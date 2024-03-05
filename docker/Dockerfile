# This is an auto generated Dockerfile for ros:desktop-full
# generated from docker_images/create_ros_image.Dockerfile.em
FROM osrf/ros:noetic-desktop-full-focal

ENV CATKIN_WS=/root/ccmslam_ws

# install ros packages
RUN apt-get update && apt-get install -y \
                      unzip \
                      python3-catkin-tools \
                      && rm -rf /var/lib/apt/lists/*

WORKDIR $CATKIN_WS

RUN catkin init && \
    catkin config \
      --extend /opt/ros/noetic

