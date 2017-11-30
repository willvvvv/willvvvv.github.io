---
title: 工厂方法模式
date: 2017-11-30 15:16:38
tags: [Pattern,JAVA]
categories: [设计模式]

---

## 类图

![](https://ws2.sinaimg.cn/large/006tKfTcgy1fm04uupnxyj30cq08w751.jpg)

## 代码

定义接口

```java
interface ISender{
    void send(String message);
}
```

实现类1

```java
class MailSenderImpl implements ISender {

    @Override
    public void send(String message) {
        System.out.println("邮件发送:" + message);
    }
}
```

实现类2

```java
class SmsSenderImpl implements ISender {
    @Override
    public void send(String message) {
        System.out.println("短信发送:" + message);
    }
}
```

定义工厂接口

```java
interface ISenderFactory{
    ISender getSender();
}
```

工厂实现1

```java
class MailSenderFactoryImpl implements ISenderFactory{
    @Override
    public ISender getSender() {
        return new MailSenderImpl();
    }
}
```

工厂实现2

```java
class SmsSenderFactoryImpl implements ISenderFactory{
    @Override
    public ISender getSender() {
        return new SmsSenderImpl();
    }
}
```

测试类

```java
class Client{
    public static void main(String args[]){
        String message = "测试内容";

        ISenderFactory factory1 = new SmsSenderFactoryImpl();
        factory1.getSender().send(message);

        ISenderFactory factory2 = new MailSenderFactoryImpl();
        factory2.getSender().send(message);
    }
}
```

## 总结

### 概述

工厂方法可以理解为，原来一个工厂是个小作坊，里面就几号人，那么造零件，造纺织品，刷漆等一系列工序都让他们做，当有一个新的职责来了，那么成本就是教会这些人去做新的事情，因为人少，所以成本低，想象一下，如果这个工厂的单子越来越多，当工厂内有新职责的时候，教学过程势必影响工厂生产，所以我们的做法就是将工厂的概念也虚化，简单来说就是成立多个工厂，有零件工厂、刷漆工厂，当有新职责来的时候就成立新的工厂，这样每个工厂的工人就只需要负责自己的职责

### 优点

更符合开闭原则
	
>当出现新职责时,简单工厂模式需要修改工厂的判断逻辑
	
单一职责原则

>简单工厂的职责并不单一

### 缺点

当新职责出现时，必须建立对应职责的工厂