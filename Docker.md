## 컨테이너 관련
- 동작중인 컨테이너 확인
> docker ps 
- 정지된 컨테이너 확인
> docker ps -a
컨테이너 삭제
> docker rm [container ID]
복수 컨테이너 삭제
> docker rm [id], [id]
컨테이너 모두 삭제
> docker rm 'docker ps -a -q'


## 이미지 관련

- 현재 이미지 확인
> docker images
- 이미지 삭제
> docker rmi [image id]
- 컨테이너 삭제 전 이미지를 삭제 + 컨테이너도 동시삭제
> docker rmi -f [image id]
