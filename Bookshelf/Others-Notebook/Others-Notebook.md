
程序员规范
---

### 项目规范

[结构化你的工程](http://pythonguidecn.readthedocs.io/zh/latest/writing/structure.html)

---

---

表情符号
---

[上网收集的表情符号](https://github.com/JNingWei/Notebook/blob/master/Bookshelf/Others-Notebook/Others-Box/Emoticon-Symbol.md)

---

---

文件后缀名
---

|   | unix系统　|　其他系统 |
| :---: | :---: | :---: |
| C源文件　|　.c | .c　| 
| C++源文件　| .cc | .cpp　| 
| C#源文件　| .cs | .cs　| 
| 头文件　| .h | .h　| 

###### P == 'PLUS' == '+'， cpp == c++

---

---

ProcessOn
---

[ProcessOn](https://www.processon.com/;jsessionid=54CAFA5DA4BE3990809758983F91DDE7.jvm1) 是一个 免费在线作图，实时协作 的绘图工具。支持流程图、思维导图、原型图、UML、网络拓扑图等。之前因为在实习公司要给项目组绘制流程图demo而用到。只能存放几张绘好的图，再多存放就要充钱了。不过只要把先前不用的成图删掉，就可以继续免费存放图了。

推荐[一篇processon教程](http://www.mamicode.com/info-detail-1615743.html)，虽然我自己并没有怎么看。。。 （─.─||）

---

---

Google Search Tip
---

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

---

---

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

### [Git常用指令备忘](https://gist.github.com/pk13610/7983917)

生成公钥：

	ssh-keygen

复制以下SSH公钥到对应地方：

	cat ~/.ssh/id_rsa.pub

测试连接是否成功：

	ssh -T git@github.com

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

---

---

Ctrl键组合
---

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

---

---

Markdown
---

最开始是因为看到网上的教程写得很简洁漂亮，所以学的Markdown。个人感觉Markdown是一种学会了就回不去的语法，特别方便简洁。

### 语法

[Markdown 语法说明 (简体中文版)](http://wowubuntu.com/markdown/index.html#list)


#### 换行

方法1: 

连续两个以上空格+回车


方法2：

使用html语言换行标签：

	<br>

#### 缩进

每个表示一个空格，连续使用两个即可表示首行缩进两个字符

	&ensp; 半角的空格
	&emsp; 全角的空格

#### 彩色字体

[字体、字号与颜色](http://mbzx.github.io/2015/09/21/md-light/)

	<font color=red>内容</font>
	
	<font color=#0099ff size=7 face="黑体">color=#0099ff size=72 face="黑体"</font>

#### 背景色

[背景色](http://www.voidcn.com/blog/testcs_dn/article/p-151884.html)

	<table><tr><td bgcolor=#7FFFD4>这里的背景色是：Aquamarine，  十六进制颜色值：#7FFFD4， rgb(127, 255, 212)</td></tr></table>

#### 图片

	<img src="图片地址" width="图片显示宽度" height="显示高度" alt="图片名称"/>
示例：

	<div align=center>
	<img src="http://ww2.sinaimg.cn/bmiddle/88070423gw1ep30aw8an7g204d04gkgd.gif" width="400" height="400" alt="亦菲表演机器猫"/>
	</div>

其中，用

	<div align=center></div>

命令进行包裹，以达到居中效果。

### 编辑器

附上一个我以前常用的轻量级的Markdown编辑器：[StackEdit](https://stackedit.io/editor)

---

---

GFM
---

GitHub 使用的是 “ GitHub Flavored Markdown ” ，简称GFM，有site-in issues,comments,pull requests等功能，它与标准的Markdown有一些区别，并增加了些新的扩展功能

Github上的一篇高star语法讲解：[README文件语法解读，即Github Flavored Markdown语法介绍](https://github.com/guodongxiaren/README)。但都是讲一些很基础的。像实际问题中遇到的四重列表嵌套外带多层中插入注释，这里面并没有讲到。

 |   | Problem | Solution |
 | --- | --- | --- |
 | 0 | 我把大段文段复制到　MarkdownEditor.io　上进行重新编辑，再贴回　github修改框　后，发现格式依然是乱的，只不过由一种乱法变成了另一种乱法。 | 上网去查，发现GFM是一种独立于Markdown的语法。在一些语法的书写上，比如列表多重嵌套，并在其中多层插入注释字段时，语法与普通的　Markdown　语法还是有很大的差别的。之前学习Markdown的时候，虽然知道Markdown有很多变种语法，但是写的都只是一些简单的嵌套，并没有涉及三四重以上的嵌套，也没有在嵌套中插入注释，所以一直没觉得GFM和Mrakdown有什么区别。直到碰上了具体情况需要这种的复杂书写时，才暴露出了这个问题。　
 | 1 | 用GFM书写简单语法时，用两个空格键就能代替Tab。空格键和Tab键常常可以多打也没关系。于是我在多重嵌套的时候依然这么干。。然后就悲剧了。。T T | 在书写GFM时想要不犯错，缩进必须要严格采用Tab键（Tab键会等于超级多个空格，远不止四个）。Tab键既不可以多打也不可以少打。 | 
 | 2 | 列表多重嵌套时，对其中某一项插入注释 | 如果注释句要与被注释的句项都是４个#字体大小的（注意：正常大小字体也会被当成前面加了4个#来识别），为了让转换器识别出这是两句从属关系的语句，则插入之前，该注释句要与被注释的句项间隔至少一行；如果注释句要与被注释的句项字体大小不一样，则可以不用空行。但是不论是哪种情况，该注释句都必须要比被注释的句项恰好多空一个Tab（只管敲Tab就好了，就算觉得每个Tab离得再宽，编辑器也会自动帮你识别清楚的；但是对列表树根进行注释时，该注释句 却不能 比被注释的句项多空一个Tab。。。没搞懂为什么会这样　T T ） | 
 | 3 | 某些时候会把语法符号也跟着显示出来，或者一些语法转换成h5时错乱 | 可能是输入时，输入状态还是处于“中文”状态下。像空格，在“中文”状态下打出的一个空格距离和“英文”状态下打出的一个空格距离是不一样的。 | 
 | 4 | 因为Markdown系列的语法最后要被转换成h5，所有可以在Markdown系列(包括GFM)文本中插入h5字段，以作为Markdown系列语法的补充，来显示出更多的效果。然而当我想在GFM写的表格中的某个空里，插入h5的代码写的列表时，发现怎么也写不出这个效果。 |  h5代码　与　GFM代码　至少间隔　一行。也就是说，Markdown系列文本的原语法字段和插入的h5字段是分开来识别的，其中前者会被转换。因而h5字段只能在全局文本的基础上插入，并不可以在原语法字段的代码中强行插入。 | 
 | 5 | 写语法时，经常会牵一发而动全身，语法错误累积多了之后，会给修改造成很大麻烦。因为任何一种显示出来的错误，都可能是多个语法错误的综合作用结果。 | 规范书写很重要！语法正确要从娃娃抓起！！ | 
 | 6 | 有时候在修改代码时，改了一个地方好像把前面字段的显示改过来了，改到后面又发现前面字段的显示重新乱了。或者是感觉后面字段的语法完全没问题，但是就是显示出来不对（比如　####　会一直被直接显示出来，或者三级列表项会一直被显示为二级列表项） | 还是因为语法错误累积得太多，牵一发而动全身。还是那句，规范书写很重要！ | 
 | 7 | 连续７个 **#** 后，无法转换成更小号的字体 | **标题字体** 相当于前面加 2 个 **#**；**正常字体** 相当于前面加 4 个 **#**；**灰色注释小字体** 相当于前面加６个 **#**；但是前面加7个以上(含7个) **#** 就转换不了了。 | 
 | 8 | 输入时，发现刚刚从句首输入的一个单字符，闪了一下又消失了 | 把前一个句法的末位字符改成以　**'英文输入状态'**　输入 | 
 | 9 | 知道可以设置代码语法高亮，但是还不知道如何设置普通字段高亮 | 等后面有空再搞 ╮(￣▽￣)╭　 | 

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

搭建翻墙代理
---

1. 进入[悠悠代理](http://www.uudaili.org/index.html)购买账号（免费账号一般都不稳定，或者限定时长，或者需要很麻烦地每天签到领流量）
	推荐买下面这种。我自己用的也是这种：
	> 普通Shadowsocks账号
	> 100/年
2. 下载[shadowsocks-qt5](https://github.com/shadowsocks/shadowsocks-qt5/wiki/Installation)客户端，通过客户端连接并创建本地代理。
3. 下载要添加到浏览器中的[SwitchyOmega](https://github.com/FelisCatus/SwitchyOmega/releases)插件。
4. 在浏览器中，根据[具体步骤](https://github.com/FelisCatus/SwitchyOmega/wiki/GFWList)来安装SwitchyOmega插件。
5. 完成

---

---

## 音频及视频端子

- ### 音频端子	
	+ #### 类比	
	+ #### 数字	

- ### 视频端子

	###### 显示屏后面一般都有一左一右两个数据接口。一个是　VGA接口　，一个是　DVI接口　。
	+ #### 类比	
		- ##### VGA
		
			###### VGA端子（Video Graphics Array (VGA) connector）。　旧电脑自带的接显示器的端口就是VGA。　
			###### VGA端子通常在电脑的显示卡、显示器及其他设备。是用作发送　模拟信号　。
	+ #### 数字	
		- ##### DVI
		
			###### DVI端子（Digital Visual Interface），中文称为“数字视频接口”。　装上GPU后，要连接上DVI线，才能从显卡中读取显示。　我实验室显示器接的就是　（DVI-D　single link） 。　
			###### DVI是一种视频接口标准，设计的目的是用来传输　未经压缩的数字化视频　。目前广泛应用于LCD、数字投影机等显示设备上。DVI接口可以发送未压缩的数字视频数据到显示设备。
			###### 视频信号
				（单通道）WUXGA 1920×1200 @ 60 Hz
				（双通道）WQXGA（2560×1600）@ 60 Hz

- ### 影音端子	
	+ #### 类比	
	+ #### 数字	


