---
title: 单例模式
date: 2017-11-30 17:18:56
tags:
	- JAVA
	- Pattern
categories: [设计模式]

---

## 类图

![](https://ws3.sinaimg.cn/large/006tKfTcgy1fm08e7g2ylj305f02jjrc.jpg)

## 代码

1.懒汉(线程不安全)

```java
class Logger1 {

    private static Logger1 instance;

    private Logger1(){}

    public static Logger1 getInstance(){
        if(instance == null){
            instance = new Logger1();
        }
        return instance;
    }
}
```

2.懒汉(线程安全)

```java
class Logger2 {

    private static Logger2 instance;

    private Logger2(){}

    public static synchronized Logger2 getInstance(){
        if(instance == null){
            instance = new Logger2();
        }
        return instance;
    }
}
```

3.饿汉

```java
class Logger3 {

    private static Logger3 instance = new Logger3();

    private Logger3(){}

    public static synchronized Logger3 getInstance(){
        return instance;
    }
}
```

4.饿汉变种

```java
class Logger4 {

    private static Logger4 instance;

    static {
        instance = new Logger4();
    }

    private Logger4(){}

    public static synchronized Logger4 getInstance(){
        return instance;
    }
}
```

5.静态内部类

```java
class Logger5 {

    private static class LoggerHolder{
        private static final Logger5 INSTANCE = new Logger5();
    }

    private Logger5(){}

    public static synchronized Logger5 getInstance(){
        return LoggerHolder.INSTANCE;
    }
}
```

测试类

```java
public class Client {
    public static void main(String args[]){

        Logger1 logger1 = Logger1.getInstance();
        Logger2 logger2 = Logger2.getInstance();
        Logger3 logger3 = Logger3.getInstance();
        Logger4 logger4 = Logger4.getInstance();
        Logger5 logger5 = Logger5.getInstance();

        System.out.println(logger1);
        System.out.println(logger2);
        System.out.println(logger3);
        System.out.println(logger4);
        System.out.println(logger5);
    }
}
```

## 总结

参考链接：[http://cantellow.iteye.com/blog/838473](http://cantellow.iteye.com/blog/838473)

### 优缺点

1.懒汉(线程不安全)

> 这种写法lazy loading很明显，但是致命的是在多线程不能正常工作。

2.懒汉(线程安全)

> 线程安全,但是效率很低,99%情况下不需要同步

3.饿汉

> 基于classloder机制避免了多线程的同步问题，但是有可能调用Singleton的其他方法，就会被初始化，没有真正达到lazy loading的效果

4.饿汉变种

> 和第三种差不多，只不过采用静态内部类的实现方式

5.静态内部类

> 真正的lazy loading的单例实现

### 其他

参考链接中还提到了其他2种实现方式，因在工作中不是特别常用，就不予以说明了

* 枚举
* 双重校验锁