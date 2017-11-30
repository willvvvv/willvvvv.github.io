---
title: 抽象工厂模式
date: 2017-11-30 16:05:18
tags: [Pattern,JAVA]
categories: [设计模式]

---

## 类图

![](https://ws3.sinaimg.cn/large/006tKfTcgy1fm06wdz2d0j30mo09mmym.jpg)

## 代码

定义鼠标接口(产品A)

```java
interface IMouse{
    void click();
}
```

定义键盘接口(产品B)

```java
interface IKeyboard{
    void press();
}
```

戴尔鼠标实现(产品A实现者1)

```java
class DellMouseImpl implements IMouse{
    @Override
    public void click() {
        System.out.println("戴尔鼠标点击");
    }
}
```

惠普鼠标实现(产品A实现者2)

```java
class HpMouseImpl implements IMouse{
    @Override
    public void click() {
        System.out.println("惠普鼠标点击");
    }
}
```

戴尔键盘实现(产品B实现者1)

```java
class HpKeyboardImpl implements IKeyboard {
    @Override
    public void press() {
        System.out.println("惠普键盘按压");
    }
}
```

惠普键盘实现(产品B实现者2)

```java
class DellKeyboardImpl implements IKeyboard{
    @Override
    public void press() {
        System.out.println("戴尔键盘按压");
    }
}
```

定义工厂接口

```java
interface IFactory{
    createMouse() : IMouse
    createKeyboard() : IKeyboard
}
```

戴尔工厂实现(工厂实现1)

```java
class DellFactoryImpl implements IFactory{

    @Override
    public IMouse createMouse() {
        return new DellMouseImpl();
    }

    @Override
    public IKeyboard createKeyboard() {
        return new DellKeyboardImpl();
    }
}
```

惠普工厂实现(工厂实现2)

```java
class HpFactoryImpl implements IFactory{

    @Override
    public IMouse createMouse() {
        return new HpMouseImpl();
    }

    @Override
    public IKeyboard createKeyboard() {
        return new HpKeyboardImpl();
    }
}
```

测试类

```java
class Client{
    public static void main(String args[]){

        //作为普通使用者，我完全可能同时使用戴尔的鼠标以及惠普的键盘
        IFactory dellFactory = new DellFactoryImpl();
        IMouse mouse = dellFactory.createMouse();

        IFactory hpFactory = new HpFactoryImpl();
        IKeyboard keyboard = hpFactory.createKeyboard();

        mouse.click();
        keyboard.press();
    }
}
```

## 总结

### 概述

抽象工厂模式实际上与工厂方法模式最大的区别就是 **多产品族**

> 工厂方法模式整体围绕单产品（文中例子出现过的ISender）

> 抽象共产围绕多产品(IMouse, IKeyWord)

### 优点

能够向客户端提供单一接口，不指定产品类型的情况下，支持生产同一个系列的不同产品

> 通过dellFactory能够直接生产dell的鼠标、键盘

### 缺点

当产品族发生变更时，违反了开闭原则

抽象产品的开闭原则有倾向性，它对不同产品体系遵循开闭，对扩展产品族违反开闭

> 可以很方便的创建一个华硕工厂、苹果工厂

> 如果要生产显示器就很方便了