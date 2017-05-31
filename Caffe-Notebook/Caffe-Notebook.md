
安装 Caffe
---

参照 [Caffe Ubuntu Installation](http://caffe.berkeleyvision.org/install_apt.html) 和 [Ubuntu 14.04上安装caffe](http://www.cnblogs.com/wm123/p/5385940.html) 即可


测试Caffe是否正常

进入 Caffe 主文件夹下

    sh data/mnist/get_mnist.sh
    sh examples/mnist/create_mnist.sh
    sh examples/mnist/train_lenet.sh
		
### Problem & Solution

#### Problem_0

    The program 'protoc' is currently not installed. You can install it by typing:
    sudo apt-get install protobuf-compiler

但是 `sudo apt-get install protobuf-compiler`  的时候又显示 protobuf-compiler 已经安装了

原因是protoc 未添入环境变量中

#### [Solution](http://www.linuxidc.com/Linux/2016-12/138716.htm)

#### Problem_1

    :~/Software/Caffe$ make all -j8
    
    PROTOC src/caffe/proto/caffe.proto
    make: protoc: Command not found
    CXX src/caffe/common.cpp
    make: *** [.build_release/src/caffe/proto/caffe.pb.h] Error 127
    make: *** Waiting for unfinished jobs....
    In file included from ./include/caffe/util/device_alternate.hpp:40:0,
    		 from ./include/caffe/common.hpp:19,
    		 from src/caffe/common.cpp:7:
    ./include/caffe/util/cudnn.hpp:8:34: fatal error: caffe/proto/caffe.pb.h: No such file or directory
    compilation terminated.
    make: *** [.build_release/src/caffe/common.o] Error 1

原因是 **protoc** 未添入 **环境变量** 中

#### [Solution](http://www.linuxidc.com/Linux/2016-12/138716.htm)

个人实际操作中，
protoc 用的是 [protobuf 发行版](https://github.com/google/protobuf/releases) 上的 protobuf-python-3.0.0.tar.gz
	‘  ./autogen.sh  ’ 执行不了，故没执行；
	‘  ./configure --prefix=/usr/local/protobuf  ’ 执行了。

#### Problem_2

 **google protobuf** 出问题

#### Solution

在[官网](http://code.google.com/p/protobuf/downloads/list)上可以下载 Protobuf 的**源代码**。然后解压编译安装便可以使用它了。

安装步骤举例如下：

     tar -xzf protobuf-2.1.0.tar.gz 
     cd protobuf-2.1.0 
     ./configure --prefix=/usr/local/protobuf
     make 
     make check 
     make install 

 添加 protobuf路径 至 环境变量 中 :
 

    sudo vim /etc/profile
添加

> export PATH=$PATH:/usr/local/protobuf/bin/ export
> PKG_CONFIG_PATH=/usr/local/protobuf/lib/pkgconfig/

保存之

    source /etc/profile

同时, 也要在 **~/.profile** 中添加上面两行代码，
否则会出现 **登录用户找不到protoc命令**

配置动态链接库路径 :

	sudo vim /etc/ld.so.conf

插入：

	/usr/local/protobuf/lib


    su  #root 权限
	ldconfig

记得要去python文件夹内（protobuf-2.1.10/python安装包下）安装python所需要的模块

	sudo python setup.py build
	sudo python setup.py test
	sudo python setup.py test

完成后，验证是否安装成功

	protoc --version
	
验证python模块是否安装成功

	python
	import google.protobuf
	
如果没有报错，则说明安装正常


----------


----------
