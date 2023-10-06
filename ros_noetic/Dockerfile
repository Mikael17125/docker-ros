FROM nvidia/cudagl:11.1.1-base-ubuntu20.04
 
# Minimal setup
RUN apt-get update \
 && apt-get install -y locales lsb-release
ARG DEBIAN_FRONTEND=noninteractive
RUN dpkg-reconfigure locales
 
# Install ROS Noetic
RUN sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
RUN apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654
RUN apt-get update \
 && apt-get install -y --no-install-recommends ros-noetic-desktop
RUN apt-get install -y --no-install-recommends python3-rosdep
RUN apt-get install -y git-all
RUN rosdep init \
 && rosdep fix-permissions \
 && rosdep update
RUN echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc
RUN apt-get install -y ros-noetic-gazebo-ros-pkgs ros-noetic-gazebo-ros-control
RUN apt-get -y install build-essential
RUN mkdir -p $HOMEcatkin_ws/src
WORKDIR /home/catkin_ws/src
RUN /bin/bash -c '. /opt/ros/noetic/setup.bash; catkin_init_workspace /home/catkin_ws/src'
RUN git clone https://github.com/ros-geographic-info/unique_identifier.git 
RUN git clone https://github.com/ros-geographic-info/geographic_info.git 
WORKDIR /home/catkin_ws
RUN /bin/bash -c '. /opt/ros/noetic/setup.bash; cd /home/catkin_ws; catkin_make'
RUN echo "source /home/catkin_ws/devel/setup.bash" >> ~/.bashrc
WORKDIR /home/catkin_ws/src
RUN git clone https://github.com/RAFALAMAO/hector_quadrotor_noetic.git
WORKDIR /home/catkin_ws
RUN /bin/bash -c '. /opt/ros/noetic/setup.bash; cd /home/catkin_ws; catkin_make'