# docker-ros-melodic-desktop

![](https://img.shields.io/docker/automated/tiryoh/ros-melodic-desktop.svg)
![](https://img.shields.io/docker/pulls/tiryoh/ros-melodic-desktop.svg)


There are official Docker images provided by OSRF.  
https://github.com/osrf/docker_images/blob/master/README.md#official-library

This image is developed to force `ubuntu` user (uid=1000, gid=1000) to run the software. If you want to run the software for other users, it is easier to use the official image.
## Docker Hub

https://hub.docker.com/r/tiryoh/ros-melodic-desktop/

## Docker tags

* base, latest
  * ros-melodic-desktop installed
  * [Dockerfile](./base/Dockerfile)
* dev
  * base + NOPASSWD
  * [Dockerfile](./dev/Dockerfile)

## Usage

* move into your ROS package, and just run:

  ```
  $ docker run --rm -it -v $(pwd):/ws tiryoh/ros-melodic-desktop catkin_make
  ```

  * `/ws` directory is simbolic linked to `/home/ubuntu/catkin_ws/src/ws`

* building ROS package `<package_name>` located in `~/workspace/ros/`:

  ```
  $ docker run --rm -it -v ~/workspace/ros/<package_name>:/home/ubuntu/catkin_ws/src/<package_name> tiryoh/ros-melodic-desktop catkin_make
  ```

## License

The Apache V2.0 License

2018 (C) Tiryoh
