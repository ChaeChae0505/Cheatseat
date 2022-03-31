# Python

### Q) [Python:error] ValueError: unsupported pickle protocol: 5
- A) version error 다 python 3.7부터 pickle 5 지원





### Tip
- list는 find가 되지 


# Pytorch
### Q) IndexError: invalid index of a 0-dim tensor. Use `tensor.item()` in Python or `tensor.item<T>()` in C++ to convert a 0-dim tensor to a number
- A) pytorch 0.5이하 에서 작성 되었던 문서를 pytorch 0.5이상으로 가져올 때 발생하는 문제 변수.data[0] --> 변수.data[]로 바꿔주면 해결가능  
  
- Error는 아니지만 UserWarning: PyTorch is not compiled with NCCL support 관련 이슈 [link](https://aigong.tistory.com/188) 이해 못함



# CPP + windows
### opengl, glew, glfw3
- vcpkg install opengl:64-windows 로 다운 받았고
- 아래 것들은 vcpkg folder 안에 넣어서 빌드하기!
- glew : https://github.com/nigels-com/glew/releases/
- glfw : https://www.glfw.org/download.html
- 압축만 풀어둠


# Ubuntu
- 인증서 관련 Error ( ssl, certificates )
- ssl error
- wget 같은 경우 --no-check-certificates 로 해결가능하지만 근본적인 문제를 해결할 수 없다
- 보통 오래된 주소를 사용하거나 , proxy 설정 인증서 오류 같은 문제로 발생한다
- 나는 해결 방법을 실행해보고 껏다 켜보지 못해서 어떤 것이 잘 되고 안 되는지 잘 모르겠다.... 순서대로 하고 꼭 재부팅을 해보자
1. [https://gitlab.com/voxl-public/system-image-build/poky/-/issues/3](https://gitlab.com/voxl-public/system-image-build/poky/-/issues/3)

2. export SSL_CERT_FILE=/usr/lib/ssl/certs/ca-certificates.crt

- [https://github.com/ros-infrastructure/rosinstall_generator/issues/40](https://github.com/ros-infrastructure/rosinstall_generator/issues/40)

3. [https://askubuntu.com/questions/73287/how-do-i-install-a-root-certificate](https://askubuntu.com/questions/73287/how-do-i-install-a-root-certificate)

- [https://askubuntu.com/questions/73287/how-do-i-install-a-root-certificate/1090617#1090617](https://askubuntu.com/questions/73287/how-do-i-install-a-root-certificate/1090617#1090617)

