# Lab4: 死锁
## 一、实验结果图
![fig1](https://github.com/liaoyaoya/ES2016_14353173/blob/master/img/deadlock.png)  
由上图可以看出，当跑到第8次就产生了死锁，无法再跑下去。
## 二、产生死锁的4个必要条件
1. 互斥条件：一个资源每次只能被一个进程使用
2. 请求与保持条件：一个进程因请求资源而阻塞时，对已获得的资源保持不放
3. 不剥夺条件:进程已获得的资源，在末使用完之前，不能强行剥夺
4. 循环等待条件:若干进程之间形成一种头尾相接的循环等待资源关系  

## 三、产生死锁的原因
本次实验代码如下：
```
class A{
	synchronized void methodA(B b){
		b.last();
	}
	synchronized void last(){
		System.out.println("Inside A.last()");
	}
}

class B{
	synchronized void methodB(A a){
		a.last();
	}
	synchronized void last(){
		System.out.println("Inside B.last()");
	}
}

class Deadlock implements Runnable{
	A a=new A();
	B b=new B();
	
	Deadlock(){
		Thread t = new Thread(this);
		int count = 20000;
		t.start();
		while(count-->0);
		a.methodA(b);
	}
	public void run(){
		b.methodB(a);
	}
	public static void main(String args[]){
		new Deadlock();
	}
}
```
根据代码，我们可以发现产生死锁的原因是：

1.  互斥条件：当synchronized用来修饰一个方法或者一个代码块的时候，能够保证在同一时刻最多只有一个线程执行该段代码。这里是a，b争夺这唯一的synchronized这个资源。  
2.  请求与保持条件：当一个线程访问object的一个synchronized同步代码块或同步方法时，其他线程对object中所有其它synchronized同步代码块或同步方法的访问将被阻塞。  
3.  不剥夺条件:当线程得到synchronized资源后，未完成都不会释放资源。  
4.  循环等待条件:若干进程之间形成一种头尾相接的循环等待资源关系。因为b中有对a的调用，而a中也有对b的调用。当t.start()启动后，run（）里面的b.methodB()就跑起来了，而等待了20000的计数后a.methodA()也会跑起来，这样跑起来的时候，因为synchronized的存在，可能会导致死锁产生了。当a.methodA(b)和b.methodB(a)同时触发时，b需要调用a.last(),但是a已经有在调用方法了，所以无法调用，同理a也无法调用b.last()，所以双方就一直在等待，造成了死锁。