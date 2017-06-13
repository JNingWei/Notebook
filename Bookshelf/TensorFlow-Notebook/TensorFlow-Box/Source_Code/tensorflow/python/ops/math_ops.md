Math
---
	
Defined in　[tensorflow/python/ops/math_ops.py](https://github.com/tensorflow/tensorflow/blob/r1.1/tensorflow/python/ops/math_ops.py)

 | op　| Args |　Annotation | 
 | --- | --- | --- | 
 | tf.add | (x, y, name=None) | 求和 | 
 | tf.subtract | (x, y, name=None) | 减法 | 
 | tf.multiply | (x, y, name=None) | 乘法 |     
 | tf.div | (x, y, name=None) | 除法 | 
 | tf.mod | (x, y, name=None) | 取模 | 
 | tf.abs | (x, name=None) | 求绝对值 | 
 | tf.negative | (x, name=None) | 取负 (y = -x). | 
 | tf.sign | (x, name=None) | 返回符号 y = sign(x) = -1 if x < 0; 0 if x == 0; 1 if x > 0. | 
 | tf.square | (x, name=None) | 计算平方 (y = x * x = x^2). | 
 | tf.round | (x, name=None) | 舍入最接近的整数  # ‘a’ is [0.9, 2.5, 2.3, -4.4] tf.round(a) ==> [ 1.0, 3.0, 2.0, -4.0 ] | 
 | tf.sqrt | (x, name=None) | 开根号 (y = \sqrt{x} = x^{1/2}). | 
 | tf.pow | (x, y, name=None) | 幂次方 # tensor ‘x’ is [[2, 2], [3, 3]] # tensor ‘y’ is [[8, 16], [2, 3]] tf.pow(x, y) ==> [[256, 65536], [9, 27]] | 
 | tf.exp | (x, name=None) | 计算e的次方 | 
 | tf.log | (x, name=None) | 计算log，一个输入计算e的ln，两输入以第二输入为底 | 
 | tf.log1p | (x, name=None) | 计算e为底的log(1+x) | 
 | tf.maximum | (x, y, name=None) | 返回最大值 (x > y ? x : y) | 
 | tf.minimum | (x, y, name=None) | 返回最小值 (x < y ? x : y) | 
 | tf.cos | (x, name=None) | 三角函数cos | 
 | tf.sin | (x, name=None) | 三角函数sin | 
 | tf.tan | (x, name=None) | 三角函数tan |  
