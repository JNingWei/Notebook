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

**第四个参数padding**：和卷积类似，可以取'VALID' 或者'SAME'. 返回一个Tensor，类型不变，shape仍然是[batch, height, width, channels]这种形式.  padding='VALID'时，无自动填充。padding='SAME'时，自动填充，池化后保持shape不变。

---

---

返回　tensor 的　维数
---

如果tensor是用调用tensorflow框架定义的，那么用 tensor_name.shape 即可返回tensorflow 的维数：

	>>> import tensorflow as tf 
	>>> a=tf.constant([  
	...         [[1.0,2.0,3.0,4.0],  
	...         　[5.0,6.0,7.0,8.0],  
	...         　[8.0,7.0,6.0,5.0],  
	...         　[4.0,3.0,2.0,1.0]],  
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

查看tensor数值
---

### 不能直接用print的原因：
print只能打印输出shape的信息，而要打印输出tensor的值，需要借助class tf.Session, class tf.InteractiveSession。

因为我们在建立graph的时候，只建立tensor的结构形状信息，并没有执行数据的操作。

### 法一：

	>>> import tensorflow as tf 
	>>> a=tf.constant([  
	...         [[1.0,2.0,3.0,4.0],  
	...         　[5.0,6.0,7.0,8.0],  
	...         　[8.0,7.0,6.0,5.0],  
	...         　[4.0,3.0,2.0,1.0]],  
	...         [[4.0,3.0,2.0,1.0],  
	...          [8.0,7.0,6.0,5.0],  
	...          [1.0,2.0,3.0,4.0],  
	...          [5.0,6.0,7.0,8.0]]  
	...     ])
	
	# Launch the graph in a session. 
	
	>>> sess = tf.Session() 
	
	# Evaluate the tensor `a`. 
	
	>>> print(sess.run(a)) 
	[[[ 1.  2.  3.  4.]
	  [ 5.  6.  7.  8.]
	  [ 8.  7.  6.  5.]
	  [ 4.  3.  2.  1.]]

	 [[ 4.  3.  2.  1.]
	  [ 8.  7.  6.  5.]
	  [ 1.  2.  3.  4.]
	  [ 5.  6.  7.  8.]]]


### 法二：


	>>> import tensorflow as tf 
	>>> a=tf.constant([  
	...         [[1.0,2.0,3.0,4.0],  
	...         　[5.0,6.0,7.0,8.0],  
	...         　[8.0,7.0,6.0,5.0],  
	...         　[4.0,3.0,2.0,1.0]],  
	...         [[4.0,3.0,2.0,1.0],  
	...          [8.0,7.0,6.0,5.0],  
	...          [1.0,2.0,3.0,4.0],  
	...          [5.0,6.0,7.0,8.0]]  
	...     ])
	
	# Launch the graph in a session. 
	
	>>> with tf.Session():
	...     print(a.eval())
	... 
 
	[[[ 1.  2.  3.  4.]
	  [ 5.  6.  7.  8.]
	  [ 8.  7.  6.  5.]
	  [ 4.  3.  2.  1.]]

	 [[ 4.  3.  2.  1.]
	  [ 8.  7.  6.  5.]
	  [ 1.  2.  3.  4.]
	  [ 5.  6.  7.  8.]]]


---

---

[tf.reshape](https://www.tensorflow.org/api_docs/python/tf/reshape)
---

reshape(
    tensor,
    shape,
    name=None
)

给定一个tensor，这个操作会返回一个有着跟原tensor一样的值且经过shape重塑过的张量。
如果shape中存在值为-1的组成，被计算过的维度总和的大小将保持恒定。尤其是当一个为[-1]的shape被展平为一维，且shape最多只能存在一个-1。
如果shape是一维或者是更高维度，那么这个操作将会返回一个形状为shape，填充满value值的张量。在这种情况下，shape的元素的数量必须与tensor的元素数量一样。

Args:

tensor: A Tensor.
shape: A Tensor. Must be one of the following types: int32, int64. Defines the shape of the output tensor.
name: A name for the operation (optional).

Returns:

A Tensor. Has the same type as tensor.


---

---

tf.nn.conv2d(input, filter, strides, padding, use_cudnn_on_gpu=None, name=None)
---

除去name参数用以指定该操作的name，与方法有关的一共五个参数：

Args|Annotation
 :---- | ----
 第一个参数input | 指需要做卷积的输入图像，它要求是一个Tensor，具有[batch, in_height, in_width, in_channels]这样的shape，具体含义是[训练时一个batch的图片数量, 图片高度, 图片宽度, 图像通道数]，注意这是一个4维的Tensor，要求类型为float32和float64其中之一
 第二个参数filter | 相当于CNN中的卷积核，它要求是一个Tensor，具有[filter_height, filter_width, in_channels, out_channels]这样的shape，具体含义是[卷积核的高度，卷积核的宽度，图像通道数，卷积核个数]，要求类型与参数input相同，有一个地方需要注意，第三维in_channels，就是参数input的第四维
第三个参数strides | 卷积时在图像每一维的步长，这是一个一维的向量，长度4
第四个参数padding | string类型的量，只能是"SAME","VALID"其中之一，这个值决定了不同的卷积方式
第五个参数 | use_cudnn_on_gpu:bool类型，是否使用cudnn加速，默认为true
---
结果返回 | 一个Tensor，这个输出，就是我们常说的feature map

---

---


