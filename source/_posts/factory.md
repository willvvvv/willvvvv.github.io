---
title: 工厂模式
date: 2017-11-30 11:06:32
tags:
	- Pattern
	- JAVA
categories: [设计模式]

---

## 类图

![](https://ws2.sinaimg.cn/large/006tKfTcgy1flzykfhm6ij308b08w74n.jpg)

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

工厂类

```java
class SenderFactory{
    public ISender getSender(Integer senderType){

        switch (senderType){
            case 1:
                return new MailSenderImpl();
            case 2:
                return new SmsSenderImpl();
            default:
                break;
        }

        return null;
    }
}
```

测试类

```java
class Client{
    public static void main(String args[]){
        SenderFactory factory = new SenderFactory();
        String message = "测试内容";
        
        //发邮件
        ISender sender1 = factory.getSender(1);
        sender1.send(message);

        //发短信
        ISender sender2 = factory.getSender(2);
        sender2.send(message);

    }
}
```

## 总结

### 优点

将对象的创建进行统一，方便维护和整体把控

### 缺点

耦合性提高,由于工厂类集中了所有实例的创建逻辑，违反了高内聚的设计原则