NumPy 是一个 Python 包。 它代表 “Numeric Python”。 它是一个由多维数组对象和用于处理数组的例程集合组成的库。

Numeric，即 NumPy 的前身，是由 Jim Hugunin 开发的。 也开发了另一个包 Numarray ，它拥有一些额外的功能。 2005年，Travis Oliphant 通过将 Numarray 的功能集成到 Numeric 包中来创建 NumPy 包。 这个开源项目有很多贡献者。

NumPy 是一个运行速度非常快的数学库，主要用于数组计算。它可以让你在 Python 中使用向量和数学矩阵，以及许多用 C 语言实现的底层函数

NumPy 的核心是数组（arrays）。具体来说是多维数组（ndarrays）

---

---

IO
---

ndarray对象可以保存到磁盘文件并从磁盘文件加载。

NumPy 为ndarray对象引入了一个简单的文件格式。 这个npy文件在磁盘文件中，存储重建ndarray所需的数据、图形、dtype和其他信息，以便正确获取数组，即使该文件在具有不同架构的另一台机器上。

### numpy.save()

load() 和 save() 函数处理 numPy 二进制文件（带 npy 扩展名）

numpy.save()文件将输入数组存储在具有npy扩展名的磁盘文件中。

    import numpy as np 
    a = np.array([1,2,3,4,5]) 
    np.save('outfile',a)

### numpy.load()  
为了从outfile.npy重建数组，请使用load()函数。

    import numpy as np 
    b = np.load('outfile.npy')  
    print b
输出如下：

    array([1, 2, 3, 4, 5])
save()和load()函数接受一个附加的布尔参数allow_pickles。 Python 中的pickle用于在保存到磁盘文件或从磁盘文件读取之前，对对象进行序列化和反序列化。


### numpy.savetxt()

### numpy.loadtxt()

loadtxt() 和 savetxt() 函数处理正常的文本文件

以简单文本文件格式存储和获取数组数据，是通过savetxt()和loadtx()函数完成的。

    import numpy as np 

    a = np.array([1,2,3,4,5]) 
    np.savetxt('out.txt',a) 
    b = np.loadtxt('out.txt')  
    print b

输出如下：

    [ 1.  2.  3.  4.  5.]

savetxt() 和 loadtxt() 接受附加的可选参数，例如页首，页尾和分隔符。

---

---

---

---


[TutorialsPoint NumPy 教程](http://www.jianshu.com/p/57e3c0a92f3a)

---

---
