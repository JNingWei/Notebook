基本网站
---

[tensorflow源码](https://github.com/tensorflow/tensorflow)

[tensorflow官网](https://www.tensorflow.org/)

[python-api](https://www.tensorflow.org/api_docs/python/)

---

---

安装
---

出处：[Ubuntu + py2.7 + gpu](https://www.tensorflow.org/install/install_linux#installing_with_native_pip)

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

tf.nn.max_pool(value, ksize, strides, padding, name=None)
---
参数是四个，和卷积很类似：

**第一个参数value**：需要池化的输入，一般池化层接在卷积层后面，所以输入通常是feature map，依然是[batch, height, width, channels]这样的shape

**第二个参数ksize**：池化窗口的大小，取一个四维向量，一般是[1, height, width, 1]，因为我们不想在batch和channels上做池化，所以这两个维度设为了1

**第三个参数strides**：和卷积类似，窗口在每一个维度上滑动的步长，一般也是[1, stride,stride, 1]

**第四个参数padding**：和卷积类似，可以取'VALID' 或者'SAME'. 返回一个Tensor，类型不变，shape仍然是[batch, height, width, channels]这种形式

---

---

返回　tensor 的　维数
---

如果tensor是用调用tensorflow框架定义的，那么用 tensor_name.shape 即可返回tensorflow 的维数：

	>>> import tensorflow as tf 
	>>> a=tf.constant([  
	...         [[1.0,2.0,3.0,4.0],  
	...         [5.0,6.0,7.0,8.0],  
	...         [8.0,7.0,6.0,5.0],  
	...         [4.0,3.0,2.0,1.0]],  
	...         [[4.0,3.0,2.0,1.0],  
	...          [8.0,7.0,6.0,5.0],  
	...          [1.0,2.0,3.0,4.0],  
	...          [5.0,6.0,7.0,8.0]]  
	...     ])
	>>> a.shape
	TensorShape([Dimension(2), Dimension(4), Dimension(4)])
也可通过调用 numpy 来返回 tensor 的维数：

	>>> import numpy as np
	>>> np.shape(a)
	TensorShape([Dimension(2), Dimension(4), Dimension(4)])



---

---


---

---


---

---


---

---


