前言
---

使用　**Ctrl** + **F** , 输入 **关键字** ，即可跳转到要查找的字段。

在熟悉　Ubuntu 后会考虑换成其他Linux系统，以从多角度理解Linux。

---

---

改源
---

> Software&Updates

 里把 源 改了，把 Other Software 改了，
随后

    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get install -f

以免以后遇到 apt-get 出现依赖 unmet 的问题。

---

---


右键添加"Open in Terminal"选项
---

如果刷的系统是正版Ubuntu，想在右键添加"Open in Terminal"选项:

    sudo apt-get install nautilus-open-terminal


----------

----------


安装 Y PPA Manager
----------------

    sudo add-apt-repository ppa:webupd8team/y-ppa-manager -y
    sudo apt-get update
    sudo apt-get install y-ppa-manager -y

在桌面左上角的 dash 直接打开


----------

----------


输入密码后又返回登录界面
------------

### [方法一](http://ubuntukylin.com/ukylin/forum.php?mod=viewthread&tid=23362)：

重装gdm

    sudo apt-get install gdm

修改启动顺序

    dpkg -reconfigure gdm

重启可登录

    sudo reboot


### 方法二：

进入了登录界面后，不用输入密码，按住 Ctrl+Alt+F1（F1～F6都行）
打开profile文件

    sudo vi /etc/profile

将多余的语句删除掉
保存修改

    :wq

重启
 

    sudo reboot

### 方法三：

输入

    startx

进入了桌面界面
编辑环境变量

    sudo gedit /etc/profile

将多余的语句删除掉, 保存
重启

    sudo reboot

在登录界面输入密码就OK了

### 方法四：
切换到 tty

> ctrl+alt+f1

    sudo rm -r .Xauthority*    # Xauthority文件在/home/用户名/.Xauthority

重启

    sudo reboot


----------

----------


装完 Cuda 重启时，输入密码后又返回登录界面
-------------------------

装 Cuda 时，如果遇到 shell 执行过程中跳出一个 **粉红色的选择框**（关于Security的选择）
这时候要选择 

> No

 因为 **Security** 会导致第三方软件不能正常安装
 **nvidia显卡的驱动** 对于 **Ubuntu** 来说就是 **第三方软件**


----------


----------

关机重启
----

关机

    sudo shutdown -h now

重启

    sudo shutdown -r now


----------


----------


安装teamviewer 远程桌面
-----------------

### [方法一](https://www.teamviewer.com/zhcn/help/363-How-do-I-install-TeamViewer-on-my-Linux-distribution.aspx):
Older systems (Ubuntu 14.04, Debian 7 and below)
Run this command:

    dpkg -i teamviewer_11.0.xxxxx_i386.deb

In case dpkg indicates missing dependencies, complete the installation by executing the following command:

    apt-get install -f

Run TeamViewer without installation
The **tar.gz** package can be run without installation and doesn’t even need root permissions.
After downloading the **tar.gz** package, you need to extract it to the directory you want to run it from. 
Simply click on “**teamviewer**” to start a TeamViewer instance.
The **tar.gz** package works, if the libraries TeamViewer depends on are installed which is often the case.
You can identify missing libraries by running the command as an administrator:

    tv-setup checklibs

**ps:**  *~/Software/teamviewer_12.0.71510_i386/opt/teamviewer/tv_bin/script/teamviewer*
Open this **.sh** file, and get how to start it.

### 方法二：

    sudo dpkg --add-architecture i386

安装i386库

    sudo apt-get install libc6:i386 libgcc1:i386 libasound2:i386 libexpat1:i386 libfontconfig1:i386 libfreetype6:i386 libjpeg62:i386 libpng12-0:i386 libsm6:i386 libxdamage1:i386 libxext6:i386 libxfixes3:i386 libxinerama1:i386 libxrandr2:i386 libxrender1:i386 libxtst6:i386 zlib1g:i386

下载teamviewer i386　

    wget http://download.teamviewer.com/download/teamviewer_i386.deb

安装teamviewer i386

    sudo dpkg -i teamviewer_i386.deb

**ps:** 一般这一步会报错，因为缺少dependencies，但是没关系，我们安装一下依赖项就可以了

     sudo apt-get update
     sudo apt-get install -f
安装完毕

#### Problem & Solution:
##### Problem_0
 > teamviewer depends on (…)

##### [Solution_0](http://askubuntu.com/questions/202247/teamviewer-depends-on-while-trying-to-install-teamviewer)
**Usage:** From the line saying "replacing" it looks as if TeamViewer is already installed.

##### Problem_1

    sudo apt-get -f install
    sudo apt-get install libc6-i386 lib32asound2 lib32z1 ia32-libs

try installing  **.deb** file with:

    sudo dpkg -i teamviewer_linux_x64.deb

If nothing works, and only if nothing works, you can force installation, but you will most probably BREAK APT:

    sudo dpkg --force-depends -i teamviewer_linux_x64.deb

----------

----------

因为您要求某些软件包保持现状，就是它们破坏了软件包间的依赖关系
-------------------------------

    sudo apt-get install aptitude

#### Problem & Solution:
找不到aptitude包, 则先

    sudo apt-get update

之后就可以 

    sudo aptitude install  ...


----------


----------


sudo apt-get update 如果出现问题
--------------------------
#### Problem & Solution:
##### Problem_0

> 以下 ID 的密钥没有可用的公钥: 1397BC53640DB551W：
> 无法下载http：//dl.google.com/linux/chrome/deb

##### Solution_0
这个是chrome仓库自己的问题

    wget -q -O - http://dl.google.com/linux/linux_signing_key.pub | sudo apt-key add -

##### Problem_1

> 无法下载 http://dl.google.com/linux/chrome/deb/dists/stable/Release 
> Unable to find expected entry 'main/binary-i386/Packages' in Release
> file (Wrong sources.list entry or malformed file Some index files
> failed to download. They have been ignored, or old ones used instead.
##### Solution_1
因为官方的Google Chrome库不再提供32位包
修改文件内容

    sudo gedit /etc/apt/sources.list.d/google-chrome.list

原来是

> deb http://dl.google.com/linux/chrome/deb/ stable main

改为：

> deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main

逐层新建 **/opt/google/chrome/cron**
打开文件

    sudo gedit /opt/google/chrome/cron/google-chrome

写入相同内容
如果本来就已经存在该文件，就输入

    sudo sed -i -e 's/deb http/deb [arch=amd64] http/' "/opt/google/chrome/cron/google-chrome"


----------


----------


apt-get 安装 出现依赖问题
-----------------

### [方法一](http://askubuntu.com/questions/140246/how-do-i-resolve-unmet-dependencies-after-adding-a-ppa)：

需要用到的部分是用了里面排名最高的回答的

> **Solutions:**

和

> **Disable/Remove/Purge PPAs:**

里的解决步骤

**ps:** 这是目前唯一一个试成了的方法

我个人实际操作时仅在

> sudo apt-get autoremove --purge package-name

一句根据具体情况做了改动
另外

> Additional Sources:

里的 **Y-PAA-Manager** 没装上，后来看来可不装

### 方法二：

更换源

> Power
>  --> System Settings 
>  --> Software&Updates 
>  --> Other Software 
>  --> add :

添加内容：

-

>    Binary
>    file:///var/cuda-repo-8-0-local
>    /
>    放空
>    放空

    
-

>    Binary
>    http://archive.ubuntukylin.com:10006/ubuntukylin
>    trusty
>    main
>    放空

-

>    Binary
>    http://dl.google.com/linux/chrome/deb/
>    stable
>    main
>    放空

-

    sudo apt-get update

删除 */var/lib/apt/lists* 下的所有文件

如果还是解决不了问题，[另寻办法](http://blog.csdn.net/supercooly/article/details/50976358)


----------


----------




安装Gnome桌面
----------

    sudo add-apt-repository ppa:tualatrix/ppa
    sudo apt-get install -f gnome-panel gnome gnome-shell gnome-menus gnome-session gdm


----------


----------


虚拟机安装改动
----

开机按 **F2**, 进入

> 高级模式 - 高级 - 处理器设置 - Intel虚拟

设置为

> 开启

**Vmare** 中 

> 设置-修改-芯片组

改为

> ICH9

----------

----------

开机自动挂载磁盘
--------

[教程](http://www.cnblogs.com/A-Song/archive/2013/02/27/2935255.html)中提醒，注意共享文件夹名称为英文，如果共享文件夹是硬盘要设置开机自动挂载

    sudo gedit /etc/fstab
    # D
    /dev/sdb1	/media/D	ntfs	defaults	0	0

---

---

局域网上的共享目录
---

	# 挂载
	sudo mount -t cifs -o username=The_username,password=The_password  Shared_directory_url  ./share

	# 卸载
	sudo umount ./share
	
另一篇同事推荐的方法：[使用Samba实现Linux与Windows文件共享实践](https://wsgzao.github.io/post/samba/)，但是我并没有试过。

### Problem & Solution

#### Problem_0

之前根据老教程，用：

sudo mount -t smbfs -o username=The_username,password=The_password  Shared_directory_url  Local_url

提示出错：
	
	mount: unknown filesystem type 'smbfs'

#### Solution

查资料后，说 smbfs 改为 cifs 了

所以改过来就可以了

----------

----------

虚拟机操作
-----

进入全屏
Super+F
点击 **显示桌面**
打开虚拟机
切换时，按下 **Super**
使用窗口切换快捷键
处理器个数不要超过实际处理器个数，否则会非常卡

如果出现

> 设备未托管

    sudo gedit /etc/NetworkManager/NetworkManager.conf

修改 

> manage=True


----------


----------

网卡设置
----

ubuntu 网卡设置,ip,mask,gateway,dns

    sudo gedit /etc/network/interfaces

这个应该是决定是否启用这个端口

> auto eth0

静态设置IP

> iface eth0 inet static
> address 172.16.146.200 netmask 255.255.255.0 broadcast 172.16.146.255
> gateway 172.16.146.254

通过dhcp动态设置

    iface eth0 inet dhcp

设置DNS服务器

    sudo vi /etc/resolv.conf

> nameserver 202.96.128.68 nameserver 61.144.56.101 nameserver
> 192.168.8.220

重新设置网络，以启用新设置

    sudo /etc/init.d/networking restart
    
修改网络配置：

    sudo gedit /etc/network/interfaces

加上

> auto eth0
> iface eth0 inet static
> address 172.18.128.28
> gateway 172.18.128.25
> netmask 255.255.255.192

重启网络设备:

    sudo /etc/init.d/network-manager restart


----------


----------


修改开机启动脚本
--------

    sudo gedit /etc/rc.local


----------


----------


修改ip
----

    sudo ifconfig eth0 172.18.128.62


----------


----------

必备软件
----

    sudo apt-get install unrar
    sudo apt-get install pure-ftpd

    sudo nautilus
    sudo apt-get install nautilus-open-terminal

    sudo service network-manager start

    sudo apt-get install mysql-server mysql-client libmysqlclient-dev

	sudo apt-get install openssh-server

----------


----------


Cannot remove entries from nonexistent file /usr/local/bin/anaconda2/lib/python2.7/site-packages/easy-install.pth
------------------------------------------------------------------------

 
删除后 **setuptools** 再运行 

    conda remove setuptools


----------


----------


pip
-------------

安装pip

    sudo apt-get install python-pip

更新pip

    pip install --upgrade pip
    
更新某个库

    pip install --upgrade ...
    pip install ... --upgrade
    pip install protobuf==3.0.0

更新所有库

    pip freeze --local | cut -d = -f 1  | xargs pip install -U


临时镜像

    pip install -i https://pypi.anaconda.org/pypi/simple ...

or

    pip install -i https://pypi.doubanio.com/simple/ ...

永久镜像

    sudo mkdir /root/.pip
    sudo gedit /root/.pip/pip.conf

添加内容

> [global] trusted-host=pypi.douban.com
> index-url=http://pypi.douban.com/simple

#### Problem & Solution:
##### Problem_0

> Failed To Download Repository Information" error:

##### Solution_0

    sudo rm -rf /var/lib/apt/lists/*
    sudo apt-get update

##### Problem_1
安装 **ipython** 时

> python setup.py egg_info的错误

##### [Solution_1](http://blog.csdn.net/cissy930426/article/details/51069324)

    pip uninstall certifi
    pip install certifi==2015.11.20
    pip install --upgrade distribute

##### Problem_2
pip can't work normally
##### Solution_2

    sudo apt-get install python python-dev libatlas-base-dev gcc gfortran g++
or
use **chown** & **chmod** to change the **authority** of python2.7

##### Problem_3
when

> sudo apt-get python-pip

can't work
##### Solution_3
try

    sudo aptitude install python-pip

choices met when install **python-pip** through **aptitude**
follow below when meet choices

> n --> y --> y


----------


----------


conda
-----
安装库

    conda install ...

更新库

    conda update ...
    
更新所有库

    conda update --all

更新 conda 自身

    conda update conda

更新 anaconda 自身

    conda update anaconda

永久镜像

    conda config --add channels 'https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/'
    conda config --set show_channel_urls yes

通过网站下载库

    anaconda search -t conda tensorflow
    anaconda show jjhelmus/tensorflow
    conda install --channel https://conda.anaconda.org/jjhelmus tensorflow

**pip** 运行的是 **anaconda** 的 python
**sudo pip** 运行的是 **系统** 的 python

----------


----------


添加权限访问声音设备
----------

将 **root** 分别添加到 **pulse组** 和 **pulse- access组**

    gpasswd -a root pulse
    gpasswd -a root pulse-access

不添加的话是没有权限访问声音设备的


----------


----------

chomd
-----
修改权限

    sudo chmod -R 777 ...


----------


----------


chown
-----

修改群组和用户

    sudo chown -hR group:users file

更改群组名

    sudo chgrp group_name file

----------


----------

find
----

    find / -name "*" -print


----------


----------

抓屏
--

    sudo apt-get install scrot
    scrot -s rectangle.png


----------


----------

中文编码
----

首行添加

	# -*- coding: utf-8 -*-

or

	#!/usr/bin/env python
	# -*- coding: utf-8 -*-


----------


----------


shadowsocks
-----------

PPA is for Ubuntu >= 14.04.

    sudo add-apt-repository ppa:hzwhuang/ss-qt5
    sudo apt-get update
    sudo apt-get install shadowsocks-qt5


----------


----------


查看库的安装版本和安装路径
-------------

左右各两根下横线

    python
    import ... as t
    t.__version__
    t.__path__


----------


----------



compress & uncompress
---------------------

### .sh
解压.sh文件

    bash ./filename.sh

or
在该文件夹下  

    ./filename.sh

### zip
压缩成zip

    zip -r archive_name.zip directory_to_compress

解压zip

    unzip archive_name.zip
    unzip file.zip -d /tmp/extract_here/

### tar
压缩成tar

    tar -cvf archive_name.tar directory_to_compress

解压tar

    tar -xvf archive_name.tar
    tar -xvf archive_name.tar -C /tmp/extract_here/

### tar.gz

压缩成tar.gz

    tar -zcvf archive_name.tar.gz directory_to_compress
    
解压tar.gz

    tar -zxvf archive_name.tar.gz 
    tar -zxvf archive_name.tar.gz -C /tmp/extract_here/

### tar.bz2

压缩成tar.bz2

    tar -jcvf archive_name.tar.bz2 directory_to_compress

解压tar.bz2

    tar -jxvf archive_name.tar.bz2 -C /tmp/extract_here/

### deb

安装deb文件

    sudo dpkg -i filename.deb 

网上找不到指定安装路径的方案

### tgz

解压tgz文件

    tar -xvzf /path/to/yourfile.tgz
    tar -xvzf /path/to/yourfile.tgz -C /path/where/to/extract/

### rar

解压rar文件

    unrar e filename.rar extract_here/

### dpkg

列出当前系统中所有的包.可以和参数less一起使用在分屏查看（类似于rpm -qa）

    dpkg -l 

查看系统中与"pkg"相关联的包（类似于rpm -qa | grep pkg）     

    dpkg -l |grep -i "pkg" 

查询一个已安装的包的详细信息（类似于rpm -qi）

    dpkg -s pkg 

查询一个已安装的软件包释放了哪些文件（类似于rpm -ql）

    dpkg -L pkg

查询系统中某个文件属于哪个软件包（类似于rpm -qf）

    dpkg -S file

查看一个未安装的deb包的详细信息（类似于rpm -qpi）

    dpkg -I pkg.deb 

手动安装软件包（不能解决软依赖性问题，可以用apt-get -f install解决）

    dpkg -i pkg.deb

卸载软件包（不是完全的卸载，它的配置文件还存在）

    dpkg -r pkg

全部卸载（不能解决依赖性的问题）

    dpkg -P pkg

将一个deb包解开至dir目录

    dpkg -x pkg.deb dir

移除多余的软件

    dpkg --pending --remove

强制安装一个包(忽略依赖及其它问题)
可以参考dpkg --force-help

    dpkg --force-all -i pkg.deb 

强制卸载一个包

    dpkg --force-all -P pkg



#### Problem & Solution
##### Problem_0

> sudo dpkg -i sogoupinyin.deb

出现依赖包的问题
##### Solution
试着用 **Ubuntu自带的 应用商店** 打开
然后重启

##### Problem_1

    tar: Exiting with failure status due to previous errors

##### Solution
修改文件权限和所属
如果行不通，则直接 右键 选择

> extract here


----------

----------


查看IP
----

    ifconfig


----------


----------

apt-get
-------

apt-cache search package    #搜索包（相当于yum list | grep pkg）
apt-cache show package      #显示包的相关信息，如说明、大小、版本等
apt-cache showpg package    #显示包的相关信息，如Reverse Depends（反向依赖）、依赖等
apt-get install package       #安装包
apt-get reinstall package     #重新安装包
apt-get -f install package    #强制安装
apt-get remove package        #删除包（只是删掉数据和可执行文件，不删除配置文件）
apt-get remove --purge package       #删除包，包括删除配置文件等
apt-get autoremove --purge package   #删除包及其依赖的软件包+配置文件等
apt-get update          #更新源
apt-get upgrade         #更新已安装的包
apt-get dist-upgrade    #升级系统
apt-get dselect-upgrade        #使用 dselect 升级
apt-cache depends package      #了解使用依赖
apt-cache rdepends package     #查看该包被哪些包依赖
apt-get build-dep package   #安装相关的编译环境
apt-get source package      #下载该包的源代码
apt-get clean && apt-get autoclean  #清理下载文件的存档 && 只清理过时的包
apt-get check             #检查是否有损坏的依赖
dpkg -S filename          #查找filename属于哪个软件包
apt-file search filename  #查找filename属于哪个软件包
apt-file list packagename #列出软件包的内容
apt-file update           #更新apt-file的数据库


----------


----------

aptitude
--------

aptitude update   #更新可用的包列表 
aptitude upgrade  #升级可用的包 
aptitude dist-upgrade     #将系统升级到新的发行版 
aptitude install pkgname  #安装包 
aptitude remove pkgname   #删除包 
aptitude purge pkgname    #删除包及其配置文件 
aptitude search string    #搜索包（相当于yum list | grep pkg，重要）
aptitude show pkgname     #显示包的详细信息 （相当于yum info pkg，重要）
aptitude clean            #删除下载的包文件 
aptitude autoclean        #仅删除过期的包文件 

aptitude与apt-get是互相补充的，有一些功能对方没有。

aptitude的优势： install， remove， reinstall（apt-get无此功能）， show（apt-get无此功能）， search（apt-get无此功能）, hold（apt-get无此功能）， unhold（apt-get无此功能）
apt-get的优势： source（aptitude无此功能）， build-dep（低版本的aptitude没有build-dep功能）
apt-get与aptitude一样的地方：update， upgrade (apt-get upgrade=aptitude safe-upgrade， apt-get dist-upgrade=aptitude full-upgrgade)
此外，如果要搜索网络上的bzip2软件包，用apt-cache search bzip2，会搜索出很多杂乱的东西，而aptitude search bzip2结果则精确的多。因为apt-cache根据全文匹配（包含描述等），而aptitude是根据文件名来匹配。


----------


----------


笔记本UBUNTU系统连不上WIFI
--------------------------------------------

[针对(Qualcomm Atheros Device)型号的无线网卡的解决方案](http://www.linuxdiyf.com/linux/26162.html)
我的无线网卡型号：  Atheros Wirelss 0042

如果你的无线网卡不是boardcom而是Qualcomm Atheros Device
 
首先告诉你为什么你的本装上Linux系统后不能连WIFI而别人的本用的同一个盘装的LINUX却可以用WIFI：
你的本的无线网卡不是boardcom博通公司产的，
而目前的UBUNTU系统装机自带的无线网卡驱动大部分都是适用于博通公司

对于高通公司的无线网卡还没有完全支持
你可以查看一下你的网卡信息：

    lspci  | grep Network  

如果显示：

> 02:00.0 Network controller: Qualcomm Atheros Device 0042 (rev 30)

表明网卡是高通的，按照以下步骤即可
 
首先连上有线网或者插上USB网卡，作如下操作：
 

下载Git和一些用来安装驱动的工具

    sudo apt-get install build-essential linux-headers-$(uname -r) git  

进行一些配置

    echo "options ath10k_core skip_otp=y" | sudo tee /etc/modprobe.d/ath10k_core.conf  

下载驱动包并解压

    wget https://www.kernel.org/pub/linux/kernel/projects/backports/2015/11/20/backports-20151120.tar.gz  
    tar zxvf backports-20151120.tar.gz  

编译，安装

    cd backports-20151120  
    make defconfig-wifi  
    make -j4
    sudo make install  

下载WIFI card并拷贝一些配置文件

    git clone https://github.com/kvalo/ath10k-firmware.git  
    sudo cp -r ath10k-firmware/QCA9377 /lib/firmware/ath10k/  
    sudo cp /lib/firmware/ath10k/QCA9377/hw1.0/firmware-5.bin_WLAN.TF.1.0-00267-1 /lib/firmware/ath10k/QCA9377/hw1.0/firmware-5.bin  


重启


----------


----------


linux查看网卡型号、驱动版本、队列数
--------------------

[详细教程](http://blog.chinaunix.net/uid-29100821-id-4139369.html)

查看网卡生产厂家和型号的基本信息 

    lspci

查看网卡生产厂家和型号的详细信息

    lspci -vvv

查看网卡驱动

    lspci -vvv

or

    lsmod

查看网卡驱动版本

    modinfo

or

    ethtool

or

    ethtool -i eth3

查看网络接口队列数

    cat /proc/interrupts | grep eth0

or

    ethtool -S eth0


----------


----------

cat
---

cat filename

----------


----------

环境变量
----

### 暂时

通过 Shell 命令 export 直接修改 Linux 环境变量
使用 export 设置的变量，只对当前终端 Shell 有效
适合设置一些临时变量

    sudo export PATH=$PATH:/usr/local/hadoop/bin

用

    echo $PATH

来查看环境配置信息

### 永久

全局环境变量，设置的是所有用户的环境

> /etc/profile /etc/bashrc /etc/environment

全局环境变量，设置的是整个系统的环境

> /etc/environment

只对单个用户生效，当用户登录时该文件仅执行一次

> ~/.bash_profile
> ~/.profile

用户可使用该文件添加自己使用的 shell 变量信息
另外在不同的LINUX操作系统下，这个文件可能是不同的
可能是 

> ~/.bash_profile 
> ~/.bash_login 
> ~/.profile

其中的一种或几种
如果存在几种的话，那么执行的顺序便是
~/.bash_profile、 ~/.bash_login、 ~/.profile
比如 Ubuntu 系统一般是 ~/.profile 文件

只对单个用户生效，当登录以及每次打开新的 shell 时，该文件被读取

> ~/.bashrc

    sudo gedit ~/.profile(or .bashrc) 

修改内容

> export PATH=/usr/local/cuda/lib64:$PATH

or

> PATH=/usr/local/cuda/bin:$PATH 
> export PATH

保存设置

    source profile

### Problem& Solution

#### Problem_0

在 /etc/profile 下修改的路径，source 完 /etc/profile 后，
关闭当前进程，
却发现新写的路径在 **新的 进程窗口** 中无法被读入

#### Solution

原因未知

在 **~/.bashrc** 文件末尾添上一句话 :

> source /etc/profile

source 该文件 :

	source ~/.bashrc 

这样每次启动该用户，都会 **自动 source 一遍** /etc/profile

----------


----------


Ubuntu 备份与恢复
------------

[详细教程](https://gist.hub.com/bearpaw/c38ef18ec45ba6548ec0)

Ubuntu可以将系统备份为一个tar压缩文件，也能很方便地从该文件恢复系统。

### 备份

我们的目标是备份/目录，但是不备份/home, 以及/proc, /sys, /mnt, /media, /run, /dev
要实现这一点，执行下列命令

    cd / 
    tar -cvpzf backup.tar.gz --exclude=/backup.tar.gz --one-file-system / 
    
其中
--exclude=/example/path: 不需要备份的文件或目录的路径
--one-file-system: 该命令能自动exclude /home, 以及/proc, /sys, /mnt, /media, /run, /dev.
/： 需要backup的partition

### 恢复

进入livecd，用gparted工具对硬盘进行分区和格式化
然后mount你想恢复的分区
一般会挂载在/mnt下
然后用下述命令恢复

    sudo mount /dev/sda2 /mnt
    sudo tar -xvpzf /path/to/backup.tar.gz -C /mnt --numeric-owner
    --numeric-owner - This option tells tar to restore the numeric owners of the files in the archive, rather than matching to any user names in the environment you are restoring from. This is due to that the user id:s in the system you want to restore don't necessarily match the system you use to restore (eg a live CD).

### 修复grub

    sudo su
    mount --bind /dev /mnt/dev
    mount --bind /dev/pts /mnt/dev/pts 
    mount --bind /proc /mnt/proc
    mount --bind /sys /mnt/sys
    chroot /mnt
    grub-install --recheck /dev/sda
    update-grub
    umout
    
    exit
    sudo umount /mnt/sys
    sudo umount /mnt/proc
    sudo umount /mnt/dev/pts
    sudo umount /mnt/dev
    sudo umount /mnt


----------


----------

关闭进程
----

    ps
    to show them all. and type:
    kill -9 PID_of_process


----------


----------

监视显存
----

监视显存使用情况

    watch [options]  command

每10秒更新一次显存使用情况

    watch -n 10 nvidia-smi


----------


----------


查看指令作用
------

    whatis command_name

for example

    $ whatis watch
    watch(1)        - execute a program periodically, showing output fullscreen


----------


----------


唐诗宋词
----

唐诗宋词package

> fortune-zh

    sudo apt-get install fortune-zh

每30秒显示一首唐诗宋词

    watch -n 30 fortune-zh


----------


----------

Google Search Tip
-----------------

限定搜索	+           
限定过滤	-           
同义词	~           
通配符	*           
精确搜索	""          
或	|           
数字范围	..          
官方定义	define      
限定文件类型	filetype    
限定网站	site        
限定新闻来源	source      
限定新闻来源国	location    
限定图片尺寸	imagesize   


----------


----------

git
---

### git规范

[Git 使用规范流程](http://www.ruanyifeng.com/blog/2015/08/git-use-process.html)

[团队中的 Git 实践](https://ourai.ws/posts/working-with-git-in-team/)

[Git: 教你如何在Commit时有话可说](https://mp.weixin.qq.com/s?__biz=MzAwNDYwNzU2MQ==&mid=401622986&idx=1&sn=470717939914b956ac372667ed23863c&scene=2&srcid=0114ZcTNyAMH8CLwTKlj6CTN&from=timeline&isappinstalled=0#wechat_redirect)

[Git工作流指南](https://github.com/xirong/my-git/blob/master/git-workflow-tutorial.md)


### git辅助工具

#### 练习工具
[git分支管理练习](http://learngitbranching.js.org/?NODEMO)

#### GUI

[sourcetree](https://www.sourcetreeapp.com/)

[tortoise](https://tortoisesvn.net/)

[smartgit](http://www.syntevo.com/smartgit/)

### github个人博客

[利用Github免费搭建个人主页(个人博客)](http://blog.csdn.net/hitwhylz/article/details/42646197)

### (Git常用指令备忘)[https://gist.github.com/pk13610/7983917]

配置：

	git config --global user.name "robbin"  
	git config --global user.email "fankai@gmail.com"
	git config --global color.ui true
	git config --global alias.co checkout
	git config --global alias.ci commit
	git config --global alias.st status
	git config --global alias.br branch
	git config --global core.editor "mate -w"    # 设置Editor使用textmate
	git config -l  # 列举所有配置

Git常用命令 查看、添加、提交、删除、找回，重置修改文件：

	git help <command>  # 显示command的help
	git show            # 显示某次提交的内容
	git show $id

	git co  -- <file>   # 抛弃工作区修改
	git co  .           # 抛弃工作区修改

	git add <file>      # 将工作文件修改提交到本地暂存区
	git add .           # 将所有修改过的工作文件提交暂存区

	git rm <file>       # 从版本库中删除文件
	git rm <file> --cached  # 从版本库中删除文件，但不删除文件

	git reset <file>    # 从暂存区恢复到工作文件
	git reset -- .      # 从暂存区恢复到工作文件
	git reset --hard    # 恢复最近一次提交过的状态，即放弃上次提交后的所有本次修改

	git ci <file>
	git ci .
	git ci -a           # 将git add, git rm和git ci等操作都合并在一起做
	git ci -am "some comments"
	git ci --amend      # 修改最后一次提交记录

	git revert <$id>    # 恢复某次提交的状态，恢复动作本身也创建了一次提交对象
	git revert HEAD     # 恢复最后一次提交的状态

查看文件diff：

	git diff <file>     # 比较当前文件和暂存区文件差异
	git diff
	git diff <$id1> <$id2>   # 比较两次提交之间的差异
	git diff <branch1>..<branch2> # 在两个分支之间比较 
	git diff --staged   # 比较暂存区和版本库差异
	git diff --cached   # 比较暂存区和版本库差异
	git diff --stat     # 仅仅比较统计信息

查看提交记录：

	git log
	git log <file>      # 查看该文件每次提交记录
	git log -p <file>   # 查看每次详细修改内容的diff
	git log -p -2       # 查看最近两次详细修改内容的diff
	git log --stat      # 查看提交统计信息
		
tig Mac上可以使用tig代替diff和log，brew install tig

分支合并和rebase：

	git merge <branch>               # 将branch分支合并到当前分支
	git merge origin/master --no-ff  # 不要Fast-Foward合并，这样可以生成merge提交

	git rebase master <branch>       # 将master rebase到branch，相当于：
	git co <branch> && git rebase master && git co master && git merge <branch>

Git补丁管理(方便在多台机器上开发同步时用)：

	git diff > ../sync.patch         # 生成补丁
	git apply ../sync.patch          # 打补丁
	git apply --check ../sync.patch  # 测试补丁能否成功

Git暂存管理：

	git stash                        # 暂存
	git stash list                   # 列所有stash
	git stash apply                  # 恢复暂存的内容
	git stash drop                   # 删除暂存区

Git远程分支管理：

	git pull                         # 抓取远程仓库所有分支更新并合并到本地
	git pull --no-ff                 # 抓取远程仓库所有分支更新并合并到本地，不要快进合并
	git fetch origin                 # 抓取远程仓库更新
	git merge origin/master          # 将远程主分支合并到本地当前分支
	git co --track origin/branch     # 跟踪某个远程分支创建相应的本地分支
	git co -b <local_branch> origin/<remote_branch>  # 基于远程分支创建本地分支，功能同上

	git push                         # push所有分支
	git push origin master           # 将本地主分支推到远程主分支
	git push -u origin master        # 将本地主分支推到远程(如无远程主分支则创建，用于初始化远程仓库)
	git push origin <local_branch>   # 创建远程分支， origin是远程仓库名
	git push origin <local_branch>:<remote_branch>  # 创建远程分支
	git push origin :<remote_branch>  #先删除本地分支(git br -d <branch>)，然后再push删除远程分支

Git远程仓库管理：

	git remote -v                    # 查看远程服务器地址和仓库名称
	git remote show origin           # 查看远程服务器仓库状态
	git remote add origin git@github:robbin/robbin_site.git         # 添加远程仓库地址
	git remote set-url origin git@github.com:robbin/robbin_site.git # 设置远程仓库地址(用于修改远程仓库地址)
	git remote rm <repository>       # 删除远程仓库

创建远程仓库：

	git clone --bare robbin_site robbin_site.git  # 用带版本的项目创建纯版本仓库
	scp -r my_project.git git@git.csdn.net:~      # 将纯仓库上传到服务器上

	mkdir robbin_site.git && cd robbin_site.git && git --bare init # 在服务器创建纯仓库
	git remote add origin git@github.com:robbin/robbin_site.git    # 设置远程仓库地址
	git push -u origin master                                      # 客户端首次提交
	git push -u origin develop  # 首次将本地develop分支提交到远程develop分支，并且track

	git remote set-head origin master   # 设置远程仓库的HEAD指向master分支
	也可以命令设置跟踪远程库和本地库

	git branch --set-upstream master origin/master
	git branch --set-upstream develop origin/develop

### Problem& Solution

#### Problem_0

> 私有秘钥必须大于4位

#### Solution

对应修改之

	git config –global user.name “robbin” 
	git config –global user.email “fankai@gmail.com” 
	git config –global color.ui true 
	git config –global alias.co checkout 
	git config –global alias.ci commit 
	git config –global alias.st status 
	git config –global alias.br branch 
	git config –global core.editor “mate -w” # 设置Editor使用textmate 
	git config -l # 列举所有配置

----------


----------

查看本机数据
--------

### 内核版本

    $ uname -a
本机内核版本： 4.4.0

    Linux hok 4.4.0-31-generic #50~14.04.1-Ubuntu SMP Wed Jul 13 01:07:32 UTC 2016 x86_64 x86_64 x86_64 GNU/Linux

### 内存
#### 方法一
查看整体内存的情况，top命令每隔几秒自动刷新

    top

#### 方法二

查看整体内存的情况，free命令的m表示以M（兆）显示，看起来很方便

    free -m

#### 方法三

查看排名前10的（改成20，30都可以）占用内存的进程

    ps -aux | sort -k4nr | head -n 10

### top

top命令是一个常用的查看系统资源使用情况和查看占用系统资源最多的进程的命令。
top以列形式显示所有的进程，占最多CPU资源的进程会显示在最上面。

要退出top或者htop，可以使用键盘快捷键Ctrl-C。
这个键盘快捷键通常会终止目前在终端上运行的进程。


### htop
htop命令是top的改进版.
默认情况下，大多数Linux发行版本都没有安装htop.
在Ubuntu系统上安装可以运行以下命令：

    sudo apt-get install htop 

htop命令显示的信息与top相同，但它的界面更人性化。
你可以使用键盘箭头键选择进程和采取某些动作，例如杀死进程或者改变它们的优先级。

### ps

ps命令可以列出正在运行的进程。
以下命令列出所有在你系统上运行的命令：

    ps -A 

这个命令列出的信息也许太多，不方便阅读。
你可以使用less命令对输出进行管道，这样你就可以按你的速度滚动阅读：

    ps -A | less 

当你阅读完后，可以按q退出。

你也可以使用grep来对输出做管道，这样可以不需要使用其它命令就能搜索出某个进程。
以下命令会搜索Firefox进程：

    ps -A | grep firefox 

### pstree

pstree命令也可以显示进程信息。
它以树的形式显示进程。
例如，你的x系统和图形环境会出现在产生树状进程的显示管理器的下面。

### kill

kill命令可以根据进程ID来杀死进程。
你可以使用ps -A，top,或者grep命令获取到进程ID。

	kill pid 

从技术层面来讲，kill命令可以发送任何信号给一个进程。
你可以使用kill -KILL或者kill -9来杀死顽固的进程。


### pgrep

给定一个搜索关键词，pgrep命令会返回所有匹配这个关键词的进程ID。	
例如，你可以使用以下命令寻找Firefox的PID:

	pgrep firefox 

你也可以将这个命令与kill命令结合起来杀死一个特定的进程。
但是，使用pkill或者killall会更简单。


### pkill & killall

pkill和killall命令可以根据进程的名字杀死一个进程。
使用以下任一方法都可以杀死Firefox进程：

    pkill firefox 
    killall firefox 


### renice

renice命令用来改变进程的nice值。
nice值代表进程的优先级。
-19的nice值是非常高的优先级，
相反，19是非常低的优先级。
0是默认的优先级。

运行renice命令需要使用进程的ID。
以下命令可以让某个进程以非常低的优先级运行:

	renice 19 pid 

你可以把pregrep和renice结合起来使用。
如果你想把进程的优先级调高，那么你需要使用root权限。
在Ubuntu系统，使用sudo获取root权限：

	sudo renice -19 # 


### xkill

xkill命令是一个可以轻易杀死图形程度的命令。
运行它之后，你的光标会变成x符号。
点击相应的图形程序的窗口就可以杀死该程序。
如果你中途要放弃操作，你可以点击鼠标右键取消。

你不一定要在终端运行这个命令——你可以在图形桌面上按Alt-F2，输入xkill然后按回车键来运行它。
我们已经将xkill和热键绑定，这样杀死进程就更容易了。

----------


----------

synaptic 图形界面下载工具
-----------------

类似于 aptitude 的图形界面下载工具：synaptic 

    sudo apt-get install synaptic


----------


----------

每次输入都会附带着删除后一格内容
----------------
#### Problem
键盘输入时，出现 “每次输入都会附带着删除后一格内容” 的问题
#### Solution
按键盘上 “Insert” 键


----------


----------

protobuf
----

### Problem & Solution

#### Problem_0

    $ conda update conda
    Traceback (most recent call last):
      File "/home/hok/anaconda2/bin/conda", line 6, in <module>
        sys.exit(conda.cli.main())
      File "/home/hok/anaconda2/lib/python2.7/site-packages/conda/cli/main.py", line 162, in main
        return conda_exception_handler(_main, *args)
      File "/home/hok/anaconda2/lib/python2.7/site-packages/conda/exceptions.py", line 630, in conda_exception_handler
        return handle_exception(e)
      File "/home/hok/anaconda2/lib/python2.7/site-packages/conda/exceptions.py", line 620, in handle_exception
        print_unexpected_error_message(e)
      File "/home/hok/anaconda2/lib/python2.7/site-packages/conda/exceptions.py", line 561, in print_unexpected_error_message
        from conda.base.context import context
      File "/home/hok/anaconda2/lib/python2.7/site-packages/conda/base/context.py", line 18, in <module>
        from .._vendor.auxlib.path import expand
      File "/home/hok/anaconda2/lib/python2.7/site-packages/conda/_vendor/auxlib/path.py", line 8, in <module>
        import pkg_resources
      File "/home/hok/anaconda2/lib/python2.7/site-packages/pkg_resources/__init__.py", line 72, in <module>
        import packaging.requirements
      File "/home/hok/anaconda2/lib/python2.7/site-packages/packaging/requirements.py", line 59, in <module>
        MARKER_EXPR = originalTextFor(MARKER_EXPR())("marker")
    TypeError: __call__() takes exactly 2 arguments (1 given)

#### Solution

将 protobuf-3.2.0 降级为 protobuf-3.1.0

    pip install --upgrade   https://storage.googleapis.com/tensorflow/linux/cpu/protobuf-3.1.0-cp27-none-linux_x86_64.whl

将 setuptools 从 35 降到 33

    pip install setuptools==33.1.1


----------


----------

搜索命令
----

### find

实际搜寻硬盘查询文件名称 

find是最常见和最强大的查找命令，你可以用它找到任何你想找的文件。
与查询数据库(/var/lib/locatedb)文件不同，find查找的是磁盘空间。

语法

    find <指定目录> <指定条件> <指定动作> 

- <指定目录>： 所要搜索的目录及其所有子目录。默认为当前目录。 
- <指定条件>： 所要搜索的文件的特征。 
- <指定动作>： 对搜索结果进行特定的处理。  

参数说明： 

时间查找参数： 

-atime n :将n*24小时内存取过的的文件列出来 
-ctime n :将n*24小时内改变、新增的文件或者目录列出来 
-mtime n :将n*24小时内修改过的文件或者目录列出来 
-newer file ：把比file还要新的文件列出来 

名称查找参数： 

-gid n       ：寻找群组ID为n的文件 
-group name  ：寻找群组名称为name的文件 
-uid n       ：寻找拥有者ID为n的文件 
-user name   ：寻找用户者名称为name的文件 
-name file   ：寻找文件名为file的文件（可以使用通配符）
		如果什么参数也不加，find默认搜索当前目录及其子目录，并且不过滤任何结果(也就是返回所有文件)，将它们全都显示在屏幕上。 

例： 
搜索当前目录(含子目录，以下同)中，所有文件名以my开头的文件。

    $ find . -name 'my*'

搜索当前目录中，所有文件名以my开头的文件，并显示它们的详细信息。 

    $ find . -name 'my*' -ls 

搜索整个磁盘系统内名为nginx的文件或目录。

    $ find / -name nginx

搜索当前目录中，所有过去10分钟中更新过的普通文件。

    $ find . -type f -mmin -10 

如果不加-type f参数，则搜索普通文件+特殊文件+目录。 

find 就是根据条件查找文件。

当我们用 whereis 和 locate 无法查找到我们需要的文件时，可以使用find，
但是find是在硬盘上遍历查 找，因此非常消耗硬盘的资源，而且效率也非常低，
因此建议大家优先使用 whereis 和 locate 。 

    
### locate

配合数据库查看文件位置 

语法：
`enter code here`locate 文件或者目录名称

例： 

搜索etc目录下所有以sh开头的文件。 

    $ locate /etc/sh

搜索用户主目录下，所有以m开头的文件。

    $ locate ~/m

搜索用户主目录下，所有以m开头的文件，并且忽略大小写。

    $ locate -i ~/m 

locate 是在数据库里查找，数据库大至每天更新一次。

locate命令其实是“find -name”的另一种写法，但是要比后者快得多，
原因在于它不搜索具体目录，而是搜索一个数据库(/var/lib/locatedb或者/var/lib/mlocate/mlocate.db)，
这个数据库中含有本地所有文件信息。
Linux系统自动创建这个数据库，并且每天自动更新一次，
所以直接使用locate命令查不到最新变动过的文件。
为了避免这种情况，可以在使用locate之前，先使用 

    update db

 命令，手动更新一下数据库。  
  
 
### whereis

查看文件的位置 

语法：

    whereis [-bmsu] 文件或者目录名称 

参数说 明： 

-b ： 只找二进制文件 
-m： 只找在说明文件manual路径下的文件 
-s ： 只找source源文件 
-u ： 没有说明文档的文件

例： 

    $ whereis grep 

whereis 可以找到可执行命令和man page 

和find相比，whereis查找的速度非常快，这是因为linux系统会将 系统内的所有文件都记录在一个数据库文件中，当使用whereis和下面即将介绍的locate时，会从数据库中查找数据，而不是像find命令那样，通 过遍历硬盘来查找，效率自然会很高。 

但是该数据库文件并不是实时更新，默认情况下时一星期更新一次，
因此，我们在用whereis和locate 查找文件时，有时会找到已经被删除的数据，或者刚刚建立文件，却无法查找到，原因就是因为数据库文件没有被更新。

whereis命令只能用于程序名的搜索，而且只搜索二进制文件(参数-b)、man说明文件(参数-m)和源代码文件(参数-s)。
如果省略参数，则返回所有信息。
同locate一样，查询数据库(/var/lib/locatedb)文件。


### which

查看可执行文件的位置 

语法：

    which 可执行文件名称

例：

    $ which grep 

which是通过 PATH环境变量到该路径内查找可执行文件，所以基本的功能是寻找可执行文件 

which命令的作用是在PATH变量指定的路径中，搜索某个系统命令的位置，并且返回第一个搜索结果。
也就是说，使用which命令，就可以看到某个系统命令是否存在，以及执行的到底是哪一个位置的命令。 


### type

type命令其实不能算查找命令，它是用来区分某个命令到底是由shell自带的，还是由shell外部的独立二进制文件提供的。
如果一个命令是外部命令，那么使用-p参数，会显示该命令的路径，相当于which命令。  

例： 

系统会提示，cd是shell的自带命令(build-in)。 

    $ type cd 

系统会提示，grep是一个外部命令，并显示该命令的路径。 

    $ type grep 

加上-p参数后，就相当于which命令。

    $ type -p grep 


----------


----------
源码安装
---

配置

    ./configure

清除编译出的新内容

	make clean

编译

	make all -j8

安装（有时候不需要）

	make install


----------


----------

环境变量
---

### Linux常见的环境变量

决定了shell将到哪些目录中寻找命令或程序：

> $PATH：

具体介绍参见后面详解。

当前用户主目录：

> $HOME：

当前用户的邮件存放目录：

>$MAIL：

当前用户用的是哪种Shell：

>$SHELL：

是指保存历史命令记录的条数

>$HISTSIZE：

当前用户的登录名:

>$LOGNAME：

主机的名称，许多应用程序如果要用到主机名的话，通常是从这个环境变量中来取得的：

>$HOSTNAME：

和语言相关的环境变量，使用多种语言的用户可以修改此环境变量：

>$LANG/LANGUGE：

基本提示符，对于root用户是#，对于普通用户是$，也可以使用一些更复杂的值：

>$PS1：

附属提示符，默认是“>”。可以通过修改此环境变量来修改当前的命令符：

>$PS2：

比如下列命令会将提示符修改成字符串 “Hello,My NewPrompt :) ” ：

	PS1=" Hello,My NewPrompt :) "
	
输入域分隔符：

>$IFS：

当shell读取输入时，用来分隔单词的一组字符，它们通常是空格、制表符和换行符。

shell脚本的名字：

>$0：

例如，在我的Linux系统中：

	$ echo $0
	/bin/bash
	
传递给脚本的参数个数：	

>$#：

shell脚本的进程号：

>$$：

脚本程序通常会用它生成一个唯一的临时文件，如

> /tmp/tmfile_$$

例如，在我的Linux系统中：

	$ echo $$
	31038               

表示当前shell进程号为31038　
	　　　　		 
### PATH
Bash shell中用export，C shell中用setenv

#### 添加环境PATH变量

> $PATH：

决定了shell将到哪些目录中寻找命令或程序，PATH的值是一系列目录，当您运行一个程序时，Linux在这些目录下进行搜寻编译链接。

    PATH=$PATH:<PATH 1>:<PATH 2>:<PATH 3>:------:<PATH N>

你可以自己加上指定的路径，中间用冒号隔开。
环境变量更改后，在用户下次登陆时生效，如果想立刻生效，则可执行下面的语句：

    source file_name

单独查看 PATH 环境变量

    echo $PATH

添加 PATH 环境变量

    export PATH=<PATH i>:$PATH
    export PATH=$PATH:<PATH i>
    export LD_LIBRARY_PATH=/home/.....(动态库的目录)

但是修改仅对 本次进程 有效

或者在相应的文档最后添上

    export PATH=<PATH i>:$PATH

退出时

    source file_name

则添加永久有效。

#### 修改环境变量

变更一个目录名 old_name

    echo ${path/old_name/new_name}   

变更所有目录名 old_name    

    echo ${path//old_name/new_name}    

#### 删除环境变量

    echo ${path#/deletion_name:}



----------


----------

Adblock沙盒
---------

进入[Adblock Fast 官网](https://adblockfast.com/)
点击

> ADD TO CHROME


----------


----------

Ctrl键组合
-------

Ctrl+A	全选
Ctrl+B	粗体
Ctrl+C	复制
Ctrl+D	添加到收藏夹
Ctrl+F	查找
Ctrl+H	历史记录
Ctrl+J	下载管理
Ctrl+K	复制目前选项卡
Ctrl+L	跳到网址栏
Ctrl+N	打开新视窗
Ctrl+O	打开旧档
Ctrl+P	打印
Ctrl+R	刷新
Ctrl+S	另存新档
Ctrl+T	开新标签页
Ctrl+V	粘贴
Ctrl+W	关闭当前选项卡（相当于Ctrl+F4）
Ctrl+X	剪切
Ctrl+Y	恢复
Ctrl+Z	撤消
Ctr++	放大
Ctrl+-	缩小


----------


----------


Markdown
---

### 语法


[Markdown 语法说明 (简体中文版)](http://wowubuntu.com/markdown/index.html#list)

### 编辑器

我以前常用的轻量级的Markdown编辑器：[StackEdit](https://stackedit.io/editor)

----

----

IPython
---

### 安装

	pip install ipython

### 打开

#### 在终端打开ipython

	ipython

#### 在网页上打开ipython

	ipython notebook

### Problem & Solution

#### Problem_0

> ImportError: No module named shutil_get_terminal_size

#### Solution

	conda config --add channels conda-forge
	conda install backports.shutil_get_terminal_size

---

---

Jupyter
---


### 安装

	pip install --upgrade pip
	pip install jupyter

### 打开

#### 在网页上打开ipython

	jupyter notebook

### Problem & Solution

#### Problem_0

When attempt to download **.ipynb** file as **.python** file:

> 500 : Internal Server Error
>
> The error was:
>
> Could not import nbconvert: cannot import name configparser

#### [Solution](https://github.com/conda/conda/issues/4823)

	conda install configparser=3.5.0b2

---

---

修改同一目录下所有图片的尺寸（宽x高）
---

	find ./ -name '*.jpg' -exec convert -resize 600x480 {} {} \;  
	find ./ -name '*.jpg' -exec convert -resize 600x480 ！{} {} \;  

---

---

生成同一目录下所有图片的路径
---

	ls *.jpg > list.txt  
	ls */train/depths/*.png > depth.txt  

---

---

查看Chrome浏览器保存的密码
---
进入URL：
> chrome://settings/passwords

将　**Saved passwords**  选项里面的密码状态设置为 **show** 

即可看到在该浏览器上保存的所有账号密码，以及该账户同步的所有账号密码

---

---
