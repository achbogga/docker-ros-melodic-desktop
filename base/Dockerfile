FROM ubuntu:focal-20230412 AS builder

RUN apt-get update && apt-get install -y curl gcc libc-dev
RUN curl -o /usr/local/bin/su-exec.c https://raw.githubusercontent.com/ncopa/su-exec/master/su-exec.c
RUN gcc -Wall /usr/local/bin/su-exec.c -o /usr/local/bin/su-exec
RUN chmod 0755 /usr/local/bin/su-exec

FROM ubuntu:focal-20230412

LABEL maintainer="aboggaram@iunu.com"

COPY --from=builder /usr/local/bin/su-exec /sbin/

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y wget curl git build-essential vim sudo lsb-release locales bash-completion && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN echo "deb http://packages.ros.org/ros/ubuntu focal main" > /etc/apt/sources.list.d/ros-latest.list && \
    curl -k https://raw.githubusercontent.com/ros/rosdistro/master/ros.key | sudo apt-key add -

RUN apt-get update && \
    apt-get install -y ros-noetic-desktop-full python3-rosdep && \
    apt-get install -y python3-rosinstall python3-rosinstall-generator python3-wstool build-essential python3-catkin-tools python3-vcstool && \
    rm -rf /var/lib/apt/lists/*

RUN rosdep init && \
    rosdep update

RUN locale-gen en_US.UTF-8
ENV LANG=en_US.UTF-8 LANGUAGE=en_US:en LC_ALL=en_US.UTF-8

COPY ./ros_entrypoint.sh /

ENTRYPOINT ["/ros_entrypoint.sh"]
CMD ["/bin/bash"]
