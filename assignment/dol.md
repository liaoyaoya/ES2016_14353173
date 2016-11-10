# Lab2: DOL实例分析与编程
## 一、Example1 的修改
### （一）实验任务
修改example1，使其输出三次方数。
### （二）修改完得到的example1.dot截图
![fig1](./example1_dot.png)
上图包含了生产者generator，平方模块（square）和消费者（consumer）三个框，还有C1和C2两条线。本次实验主要修改的是平方模块的内容，但因为没有改变名字，所以修改前后的dot图是一致的。
### （三）实验过程
1. 在square.c文件中的square_fire信号处理函数，读入输入端信号i，原来是将其平方后写出到输出端，重复length次后停止。因为要求输出三次方数所以就把原来的`i=i*i;` 变成了三个i相乘即可：`i=i*i*i;`
 实验截图如下：
 ![fig2](./example1_square.png)
2. 重新编译运行example1
    ```    
	$ sudo ant -f build_zip.xml all
    $ sudo ant –f runexample.xml –Dnumber=1
    ```
3. example1运行后的结果如下图所示:  
   ![fig3](./example1.png)
	从上到下0~19的三次方数。 
## 二、Example2 的修改
### （一）实验任务
修改example2，让3个square模块变成2个
### （二）修改完得到的example2.dot截图
![fig4](./example2_dot.png)
上图包含了生产者generator，两个平方模块（square）和消费者（consumer）四个框，还有C2_0, C2_1 和 C2_2 三条线。本次实验主要修改的是square模块的数量，从三个变成两个。
### （三）实验过程
1. example2.xml文件中定了迭代数，所以实验中就应该把该文件下的`<variable value="3" name="N">` 改成`<variable value="2" name="N">` ，因为这个value的值就会是square模块的迭代数。
 实验截图如下：
 ![fig5](./example2_xml.png)

2. 重新编译运行example1
    ```    
	$ sudo ant -f build_zip.xml all
    $ sudo ant –f runexample.xml –Dnumber=2
    ```
3. example1运行后的结果如下图所示:  
   ![Alt text](./example2.png)
   从上到下0~19的四次方数，因为这是两个square模块迭代得到的值，一个square是`i=i*i`，那么两个square迭代后就会使`i=i^4`,如果是原来的三个square模块结果就会使`i=i^8`
## 三、实验感想与心得
1. example中各文件的含义如下：
    src文件夹：各进程（生产者，消费者，处理模块等）的功能定义
    example1.xml：系统架构即模块连接方式定义。
2. 所以本次实验主要是要理解生产者给处理模块输入数据，然后处理模块根据定义的内容功能来处理数据后往下一个模块输出，最后消费者获得的就是经过所有处理模块处理的数据了。
3. 对于处理模块，每迭代一次，就会相当于增加一个同样的模块，也就是把数据再用同样的方法处理一遍。
