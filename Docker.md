## docker install
- [docker documents](https://docs.docker.com/engine/install/ubuntu/)
- [NVIDIA docker](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html#docker)

```
안깔리면
$ curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | \
  sudo tee /etc/apt/sources.list.d/nvidia-docker.list # 추가
  
# https://github.com/NVIDIA/nvidia-docker/issues/716
```


## docker 명령어
- docker using without sudo 
```
sudo usermod -aG docker $USER
```

```
도커그룹생성
sudo groupadd docker

도커그룹에 유저추가
sudo usermod -aG docker ${USER}
or
sudo gpasswd -a $USER docker

도커 재시작
sudo service docker restart

현재 사용자 로그아웃 및 재로그인
sudo su - // 루트사용자로 변경
su - ubuntu // 사용자로 변경

테스트
docker run hello-world
```

## 컨테이너 관련
- 동작중인 컨테이너 확인
```docker ps```
- 정지된 컨테이너 확인
```docker ps -a```
- 컨테이너 삭제
```docker rm [container ID]```
- 복수 컨테이너 삭제
```docker rm [id], [id]```  
- 컨테이너 모두 삭제
```docker rm 'docker ps -a -q' ```


## 이미지 관련

- 현재 이미지 확인
```docker images```
- 이미지 삭제
```docker rmi [image id]```
- 컨테이너 삭제 전 이미지를 삭제 + 컨테이너도 동시삭제
```docker rmi -f [image id]```


## Docker 이미지를 registry 거치지 않고 이동하고 싶을 때 

1. docker save (docker image -> tar)
- docker 이미지를 tar파일로 저장하기 위해서는 docker save 커맨드를 사용한다.
```
docker save \[옵션\] <파일명> \[이미지명\]
```
- 저장할 파일명을 지정하는 옵션은 -o 를 사용한다.
```
ex) docker save -o nginx.tar nginx:latest
```

2. docker load (tar -> docker image)
- tar파일로 만들어진 이미지를 다시 docker image로 되돌리기 위해서는 docker load 커맨드를 사용한다.
```
docker load -i tar파일명
```

3. docker export (docker container -> tar)
- docker는 이미지 뿐 아니라 container를 tar파일로 저장하는 명령어를 제공한다.
```
docker export <컨테이너명 or 컨테이너ID> > xxx.tar
``` 

4. docker import (tar -> docker image)
- export 커맨드를 통해 만들어진 tar 파일을 다시 docker image로 생성하는 명령어이다.
```
docker import <파일 or URL> - \[image name\[:tag name\]\]
```
※ root 권한으로 실행하지 않을 경우, 액세스 권한이 없는 파일들이 포함되지 않는 문제가 발생할 수 있다.

 
```
(중요) export - import 와 save - load의 차이

docker export의 경우 컨테이너를 동작하는데 필요한 모든 파일이 압충된다. 즉, tar파일에 컨테이너의 루트 파일시스템 전체가 들어있는 것이다.반면에 docker save는 레이어 구조까지 포함한 형태로 압축이 된다.

즉, 기반이 되는 이미지가 같더라도 export와 save는 압축되는 파일 구조와 디렉터리가 다르다.
save 로 저장하면 레이어로 저장이 되고 export 로 저장하면 디렉토리를 볼 수 있다!!!

결론은export를 통해 생성한 tar 파일은 import로, save로 생성한 파일은 load로이미지화 해야 한다.
```

## Docker 컨테이너에서 변경한 사항 -> 다른 이미지로 저장
```
# docker images check
sudo docker images 

# Image 실행
sudo docker run -it <images name>

# docker 수정

# docker를 실행한 채로
# 다른 터미널에서 
sudo docker ps

# Container ID 항목 복사
sudo docker commit <container ID> <New image save name>

# 이미지 실행가능해짐
```

## tmux
```
apt-get install tmux
tmux

* 모든 명령어는 ctrl + b 와 함께 실행
* ctrl + D는 창을 빠져나올 때


```



# Docker error
- Q) docker nvidia 16.04 version에서 ubuntu 16.04 E: Couldn't find any package by regex 'python3.7-dev'
- A) 지원 안한다 그냥 18.04 쓰자[해결자세히](https://somjang.tistory.com/entry/Docker-ubuntu1604-%EC%97%90%EC%84%9C-deadsnakes-PPA%EB%A5%BC-%ED%86%B5%ED%95%9C-Python-%EC%84%A4%EC%B9%98-%EC%A7%80%EC%9B%90-%EC%A2%85%EB%A3%8C-%EB%B0%8F-%ED%95%B4%EA%B2%B0-%EB%B0%A9%EB%B2%95) 



# 자주 참고하는 docker repo
- melodic [openvins](https://hub.docker.com/r/celinachild/openvslam)
```
$ docker pull celinachild/openvslam:latest

$ docker run --gpus all -it --ipc=host --net=host --privileged -e DISPLAY=unix$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix:rw -e NVIDIA_DRIVER_CAPABILITIES=all celinachild/openvslam 


# for mapping
$ ./run_video_slam -v ./orb_vocab/orb_vocab.dbow2 -m ./aist_living_lab_1/video.mp4 -c ./aist_living_lab_1/config.yaml --no-sleep --map-db map.msg

# for localization
$ ./run_video_localization -v ./orb_vocab/orb_vocab.dbow2 -m ./aist_living_lab_2/video.mp4 -c ./aist_living_lab_2/config.yaml --no-sleep --map-db map.msg
```


- 이 repo에는 ros가 없다
```
apt-get update
apt-get install lsb -y


sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
apt install curl # if you haven't already installed curl
curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | apt-key add -
apt update
apt install ros-melodic-desktop-full



echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc
source ~/.bashrc
apt install python-rosdep python-rosinstall python-rosinstall-generator python-wstool build-essential


apt install python-rosdep
rosdep init
rosdep update



echo "eb='gedit ~/.bashrc'" >> ~/.bashrc
echo "sb='source ~/.bashrc'" >> ~/.bashrc
```

## ERROR
- 내부에서 apt repo로 다운 하려고 하는데 404 error :: apt-get update



## Docker script 실행
- [check](https://swiftcam.tistory.com/537)
