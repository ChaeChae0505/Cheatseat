# Python

- Q) [Python:error] ValueError: unsupported pickle protocol: 5
- A) version error 다 python 3.7부터 pickle 5 지원


- Q) /usr/bin/bash: /home/ch/anaconda3/envs/rlgpu/lib/libtinfo.so.6: no version information available (required by /usr/bin/bash)
- A) 



# Pytorch
- Q) IndexError: invalid index of a 0-dim tensor. Use `tensor.item()` in Python or `tensor.item<T>()` in C++ to convert a 0-dim tensor to a number
- A) pytorch 0.5이하 에서 작성 되었던 문서를 pytorch 0.5이상으로 가져올 때 발생하는 문제 변수.data[0] --> 변수.data[]로 바꿔주면 해결가능
