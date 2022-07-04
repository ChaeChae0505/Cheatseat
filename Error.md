# Python

#### Q) [Python:error] ValueError: unsupported pickle protocol: 5
- A) version error 다 python 3.7부터 pickle 5 지원





#### Tip
- list는 find가 되지 


# Pytorch
#### Q) IndexError: invalid index of a 0-dim tensor. Use `tensor.item()` in Python or `tensor.item<T>()` in C++ to convert a 0-dim tensor to a number
- A) pytorch 0.5이하 에서 작성 되었던 문서를 pytorch 0.5이상으로 가져올 때 발생하는 문제 변수.data[0] --> 변수.data[]로 바꿔주면 해결가능  
  
- Error는 아니지만 UserWarning: PyTorch is not compiled with NCCL support 관련 이슈 [link](https://aigong.tistory.com/188) 이해 못함



# CPP + windows
#### opengl, glew, glfw3
- vcpkg install opengl:64-windows 로 다운 받았고
- 아래 것들은 vcpkg folder 안에 넣어서 빌드하기!
- glew : https://github.com/nigels-com/glew/releases/
- glfw : https://www.glfw.org/download.html
- 압축만 풀어둠


# Ubuntu
#### 인증서 관련 Error ( ssl, certificates )
- ssl error
- wget 같은 경우 --no-check-certificates 로 해결가능하지만 근본적인 문제를 해결할 수 없다
- 보통 오래된 주소를 사용하거나 , proxy 설정 인증서 오류 같은 문제로 발생한다
- 나는 해결 방법을 실행해보고 껏다 켜보지 못해서 어떤 것이 잘 되고 안 되는지 잘 모르겠다.... 순서대로 하고 꼭 재부팅을 해보자
1. [https://gitlab.com/voxl-public/system-image-build/poky/-/issues/3](https://gitlab.com/voxl-public/system-image-build/poky/-/issues/3)

2. export SSL_CERT_FILE=/usr/lib/ssl/certs/ca-certificates.crt

- [https://github.com/ros-infrastructure/rosinstall_generator/issues/40](https://github.com/ros-infrastructure/rosinstall_generator/issues/40)

3. [https://askubuntu.com/questions/73287/how-do-i-install-a-root-certificate](https://askubuntu.com/questions/73287/how-do-i-install-a-root-certificate)

- [https://askubuntu.com/questions/73287/how-do-i-install-a-root-certificate/1090617#1090617](https://askubuntu.com/questions/73287/how-do-i-install-a-root-certificate/1090617#1090617)

#### library를 못 찾아!
- rviz: error while loading shared libraries: libconsole_bridge.so.1.0: cannot open shared object file: No such file or directory
1. 위치를 찾는다
```shell
$ ldconfig -p | grep libconsol* 
$ dpkg -L openjdk-8-jre
```

2. LD_LIBRARY_PATH로 연결 (bashrc)
```shell
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda-11.6/lib64:/opt/ros/noetic:/usr/lib/x86_64-linux-gnu
```
#### Error) qtplugin을 찾을 수 없다는 에러가 떳다
- apt install libxcb-xinerama0 을 하니 이미 설치 되있다고 했다
- 그래서 coppeliasim으로 qt plugin path 지정된 것을 해제했더니 가능했다


# ROS
#### E) Gazebo [err] [REST.cc:205] Error in REST request error
- home에서 .ignition/fuel/config.yaml을 켜준다
- $ gedit .ignition/fuel/config.yaml
```
---
# The list of servers.
servers:
  -
    name: osrf
    #url: https://api.ignitionfuel.org >>를 아래 url로 변경해줌
    url: https://api.ignitionrobotics.org

  # -
    # name: another_server
    # url: https://myserver

# Where are the assets stored in disk.
# cache:
#   path: /tmp/ignition/fuel
```
#### E) conda환경에서 build하려고 할때! catkin_pkg modulenotfound err
- conda install -c auto catkin_pkg
- pip install catkin_pkg


# CMAKE error
## build 시 cuda error
`-O3 -gencode arch=compute_62,code=sm_62`  이런식으로 cmake list에 추가 하면 된다는데? [https://en.wikipedia.org/wiki/CUDA#Supported_GPUs](https://en.wikipedia.org/wiki/CUDA#Supported_GPUs)

- cuda cmake 연결
    
    ```python
    # Find CUDA
    find_package(CUDA QUIET)
    if (CUDA_FOUND)
      find_package(CUDA REQUIRED)
      message(STATUS "CUDA Version: ${CUDA_VERSION_STRINGS}")
      message(STATUS "CUDA Libararies: ${CUDA_LIBRARIES}")
      set(
        CUDA_NVCC_FLAGS
        ${CUDA_NVCC_FLAGS};
        -O3
        -gencode arch=compute_30,code=sm_30
        -gencode arch=compute_35,code=sm_35
        -gencode arch=compute_50,code=[sm_50,compute_50]
        -gencode arch=compute_52,code=[sm_52,compute_52]
        -gencode arch=compute_61,code=sm_61
        -gencode arch=compute_62,code=sm_62
      )
      add_definitions(-DGPU)
    else()
      list(APPEND LIBRARIES "m")
    endif()
    ```
    

[https://arnon.dk/matching-sm-architectures-arch-and-gencode-for-various-nvidia-cards/](https://arnon.dk/matching-sm-architectures-arch-and-gencode-for-various-nvidia-cards/)

30어쩌고 지원 안된다해서 그부분 지워 줌 cuda nvcc flage에서
