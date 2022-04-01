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



# Docker error
- Q) docker nvidia 16.04 version에서 ubuntu 16.04 E: Couldn't find any package by regex 'python3.7-dev'
- A) 지원 안한다 그냥 18.04 쓰자[해결자세히](https://somjang.tistory.com/entry/Docker-ubuntu1604-%EC%97%90%EC%84%9C-deadsnakes-PPA%EB%A5%BC-%ED%86%B5%ED%95%9C-Python-%EC%84%A4%EC%B9%98-%EC%A7%80%EC%9B%90-%EC%A2%85%EB%A3%8C-%EB%B0%8F-%ED%95%B4%EA%B2%B0-%EB%B0%A9%EB%B2%95) 
