FROM nvcr.io/nvidia/l4t-pytorch:r32.7.1-pth1.10-py3
LABEL maintainer="achbogga@gmail.com"
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 42D5A192B819C5DA
RUN apt-get update -q && \
    apt-get install --no-install-recommends -yq curl && \
    apt-get install --no-install-recommends -yq gcc libc-dev && \
    rm -rf /var/lib/apt/lists/*

RUN apt-get update -q && \
    apt-get upgrade -yq --no-install-recommends && \
    apt-get install -yq --no-install-recommends wget curl git build-essential vim sudo lsb-release locales bash-completion

RUN sh -c 'echo "deb http://packages.ros.org/ros/ubuntu bionic main" > /etc/apt/sources.list.d/ros-latest.list'
RUN curl -k https://raw.githubusercontent.com/ros/rosdistro/master/ros.key | sudo apt-key add -
RUN apt-get update -q && \
    apt-get install --no-install-recommends -y ros-melodic-desktop-full python-rosdep && \
    apt-get install --no-install-recommends -y python-rosinstall python-rosinstall-generator python-wstool build-essential python-catkin-tools python3-vcstool
RUN apt-get install -yq --no-install-recommends python3-pip && \
    apt install -yq --no-install-recommends python3-rospkg
RUN apt install ros-melodic-desktop-full --fix-missing && \
    rm -rf /var/lib/apt/lists/*
RUN rosdep init
RUN locale-gen en_US.UTF-8
ENV LANG=en_US.UTF-8 LANGUAGE=en_US:en LC_ALL=en_US.UTF-8
RUN rosdep update
COPY ./ros_entrypoint.sh /
ENTRYPOINT ["/ros_entrypoint.sh"]
CMD ["/bin/bash"]
