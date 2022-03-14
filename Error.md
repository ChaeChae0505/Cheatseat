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
