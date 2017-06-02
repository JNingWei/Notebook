
[安装](http://docs.opencv.org/trunk/d7/d9f/tutorial_linux_install.html)
---

### Problem & Solution
#### Problem_0
apt-get 下不了
#### Solution
用aptitude下

#### Problem_1
ffmpeg下不到
#### Solution
硬盘 **opencv 文件夹** 下面有 **ffmpeg 压缩包**
在终端下解压即可
无需制定目录，也无需再复制转移

#### Problem_2

> /home/zwn/caffe/caffe-install/Install-OpenCV-master/Ubuntu/2.4/OpenCV/opencv-2.4.9/modules/gpu/src/nvidia/core/NCVPixelOperations.hpp(51):
> error: a storage class is not allowed in an explicit specialization

#### [Solution](http://code.opencv.org/issues/3814)

下载 NCVPixelOperations.hpp 替换掉opencv2.4.9内的文件
重新
buildUnsupported gpu architecture 'compute_11
硬盘的 **CUDA文档** 里面有**备份**

#### Problem_3
在一个关于opencv_vedio的地方出错。
#### Solution
在语句中添加一句话
在硬盘的 **opencv文件夹** 中的安装教程已经修改
并进行了中文注释

#### Problem_4
**opencv2.4.9** 只有在遇到 **CUDA8.0** 的时候才会出现的问题
如果 **CUDA** 是 **7.5** 就不会出现这个问题

> modules/cudalegacy/src/graphcuts.cpp:120:54: error: 
> ‘NppiGraphcutState’ has not been declared typedef NppStatus
> (*init_func_t)(NppiSize oSize,  NppiGraphcutState** ppState, Npp8u*
> pDeviceMem);

#### [Solution](http://blog.csdn.net/xuzhongxiong/article/details/5271728)
按照硬盘里面 **opencv文件夹** 下的图片
修改以下文件的内容 

> ～/OpenCV/opencv-2.4.9/modules/gpu/src/graphcuts.cpp

#### Problem_5
在ubuntu service 14.04 下搭建 OpenCL +OpenCV 环境
前期安装了 CUDA7.0 ，GPU 为 NVIDIA TITAN

> Unsupported gpu architecture 'compute_11 nvcc fatal   : Unsupported
> gpu architecture 'compute_11' CMake Error at
> cuda_compile_generated_matrix_operations.cu.o.cmake:206 (message):  
> Error generating
> /home/smie/Documents/opencv2.4.11/build/modules/core/CMakeFiles/cuda_compile.dir/__/dynamicuda/src/cuda/./cuda_compile_gene
> 
> rated_matrix_operations.cu.o
> 
> make[2]: ***
> [modules/core/CMakeFiles/cuda_compile.dir/__/dynamicuda/src/cuda/./cuda_compile_generated_matrix_operations.cu.o] Error 1 make[1]: *** [modules/core/CMakeFiles/opencv_core.dir/all]
> Error 2 make[1]: *** Waiting for unfinished jobs....

#### Solution
When using cmake to do configurations, set the option CUDA_GENERATION to specific your GPU architecture. 

> CUDA_GENERATION: cmake -D CMAKE_BUILD_TYPE=RELEASE -D
> CMAKE_INSTALL_PREFIX=/usr/local -D CUDA_GENERATION=Kepler ..


#### Problem_6

opencv 有时候会被装到 

> /usr/local/lib/python2.7/dist-packages

#### Solution
只要把里面的 **cv.py** 、**cv2.so** 这两个文件拷进

> ~/anaconda2/lib/python2.7/site-packages

就能在 anaconda下的 python2.7 中调用了


----------


----------
