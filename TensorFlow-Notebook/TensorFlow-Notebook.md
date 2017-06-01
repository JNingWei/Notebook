[py2.7+gpu 安装tensorflow](https://www.tensorflow.org/install/install_linux#installing_with_native_pip)
---

pip uninstall tensorflow
pip install tensorflow-gpu

tensorflow 尽量从 **源码** 安装，这样运行起来会更快，遇到的 Warning 也更少

### Problem & Solution

#### Problem_0

如果 TensorFlow 程序运行缓慢， 可能和 protobuf pip package 有关

#### Solution

    pip install --upgrade https://storage.googleapis.com/tensorflow/linux/cpu/protobuf-3.1.0-cp27-none-linux_x86_64.whl
	  
	  

----------


----------

[Tensorflow一些常用基本概念与函数](http://blog.csdn.net/lenbow/article/category/6194008)
---

---

---
