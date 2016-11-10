# README
## 一、DOL 框架描述
DOL(The distributed operation layer)是一个用于编写并行应用程序的软件开发框架。DOL允许指定基于计算Kahn进程网络模型的应用程序和具有一个基于SystemC的模拟引擎的特点。而且，DOL提供了一个基于XML规范的格式来描述在一个多处理器系统上的并行应用程序的实现，包括它的捆绑和映射。
## 二、DOL 安装笔记
在VMware虚拟机中的Ubuntu16.04系统下，打开terminal，输入指令，完成环境的配置。
### （一）安装一些必要的环境
```
$	sudo apt-get update
$	sudo apt-get install ant
$ 	sudo apt-get install openjdk-7-jdk
$	sudo apt-get install unzip
```
在跑`$ 	sudo apt-get install openjdk-7-jdk` 这句代码时，出现了报错	 
错误信息：  
![fig1](https://github.com/liaoyaoya/ES2016_14353173/blob/master/img/fig1.png)   
解决方法：因为Ubuntu16.04的安装源中已经默认没有openjdk-7了，所以需要我们自己手动添加到仓库中
```
$	sudo add-apt-repository ppa:openjdk-r/ppa
$	sudo apt-get update
$	sudo apt-get install openjdk-7-jdk  
```

### （二）下载文件(直接用了命令行下载)
```
sudo wget http://www.accellera.org/images/downloads/standards/systemc/systemc-2.3.1.tgz

sudo wget http://www.tik.ee.ethz.ch/~shapes/downloads/dol_ethz.zip
```
### （三）解压文件
1. 新建dol的文件夹:`$	mkdir dol`
2. 将dol_ethz.zip解压到dol文件夹中:`$	unzip dol_ethz.zip -d dol`
3. 解压systemc:`$	tar -zxvf systemc-2.3.1.tgz`

### （四）编译systemc
1. 解压后进入systemc-2.3.1的目录下:  
 `$	cd systemc-2.3.1`
2. 新建一个临时文件夹obidir并进入该文件夹objdir:  
		`$	mkdir obidir`   
		`$	cd obidir`
3. 运行configure（能根据系统的环境配置一下参数，用于编译）  
`$	../configure CXX=g++ --disable-async-updates`

    运行后出来得到截图如下，无误后就可以继续往下了：  
![fig2](https://github.com/liaoyaoya/ES2016_14353173/blob/master/img/fig2.png)

4. 编译  
		`$	sudo make install`
5. 编译完后打开文件目录  
		`$	cd ..`  
		`$	ls`
		
    得到的文件目录如下：  
![fig3](https://github.com/liaoyaoya/ES2016_14353173/blob/master/img/fig3.png)

6. 记录下当前的（输出的）工作路径，待会会用到  
		`$	pwd`  
![fig4](https://github.com/liaoyaoya/ES2016_14353173/blob/master/img/fig4.png)  
由上图可知我当前的工作路径为:  
`/home/liaoyaoya/systemc-2.3.1`

### （五）编译dol
1. 进入刚刚新建的dol文件夹`$	cd ../dol`
2. 修改build_zip.xml文件（因为是64位系统的机器，所以lib-linux要改成lib-linux64）
遇到的问题：build_zip.xml文件不让修改，无法保存修改的东西  
解决：`$	sudo gedit build_zip.xml`  
修改如下：  
![fig5](https://github.com/liaoyaoya/ES2016_14353173/blob/master/img/fig5.PNG)
3. 编译`$	ant -f build_zip.xml all`

### （六）试跑第一个例子
1. 进入/build/bin/main路径下：`$	cd build/bin/main`
2. 运行第一个例子：`$	sudo ant -f runexample.xml -Dnumber=1`
    第一次build failed了：  
![fig6](https://github.com/liaoyaoya/ES2016_14353173/blob/master/img/fig6.png)  
    解决方法：因为安装了多个版本的JAVA，需要设置一下JAVA的环境变量`$	sudo update-alternatives --config java`  
![fig7](./fig7.png)  
    然后选择对应的java-z-openjdk-amd64那一项，即是上图中选项1那一项。再运行一次`$	sudo ant -f runexample.xml -Dnumber=1`
    BUILD SUCCESSFUL结果图如下：  
![fig8](https://github.com/liaoyaoya/ES2016_14353173/blob/master/img/fig8.png)
3. 在build/bin/main/example1文件夹中有一个example1.dot文件，双击点开得到下图：  
![dot](https://github.com/liaoyaoya/ES2016_14353173/blob/master/img/dot.PNG)


## 三、实验感想与心得
1. 使用markdown语法来写真的非常方便不需要排版，已经自动排好了。
2. 在配置DOL的环境时，确实有不少的问题出现，但是结合TA提供的Q&A和网上的资料，还是比较容易解决的。
