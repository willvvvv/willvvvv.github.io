---
title: 建造者模式
tags:
  - JAVA
  - Pattern
categories:
  - 设计模式
date: 2017-11-30 20:27:06

---

## 类图

![](https://ws1.sinaimg.cn/large/006tNc79gy1fm0du2jhnnj30810abwf1.jpg)

## 代码

车类

```java
class Car{

    /**
     * 轮胎
     */
    private String tire;

    /**
     * 发动机
     */
    private String engine;

    public void setTire(String tire) {
        this.tire = tire;
    }

    public void setEngine(String engine) {
        this.engine = engine;
    }

    @Override
    public String toString() {
        return "Car{" +
                "tire='" + tire + '\'' +
                ", engine='" + engine + '\'' +
                '}';
    }
}
```

建造接口

```java
interface Builder{

    void buildTire();

    void buildEngine();

    Car getCar();

}
```

奥迪建造工艺

```java
class AudiBuilder implements Builder{

    private Car car = new Car();

    @Override
    public void buildTire() {
        car.setTire("米其林轮胎");
    }

    @Override
    public void buildEngine() {
        car.setEngine("A6L 2.0L");
    }

    @Override
    public Car getCar() {
        return car;
    }
}
```

宝马建造工艺

```java
class BMWBuilder implements Builder{

    private Car car = new Car();

    @Override
    public void buildTire() {
        car.setTire("马牌轮胎");
    }

    @Override
    public void buildEngine() {
        car.setEngine("3x 1.5T");
    }

    @Override
    public Car getCar() {
        return car;
    }

}
```

造车工厂

```java
class CarFactory{

    private Builder builder;

    public CarFactory(Builder builder) {
        this.builder = builder;
        builder.buildTire();
        builder.buildEngine();
    }

    public Builder getBuilder() {
        return builder;
    }
}
```

测试类

```java
public class Client {

    public static void main(String args[]){
        Builder audiBuilder = new AudiBuilder();
        Builder BMWBuilder = new BMWBuilder();

        CarFactory factory = new CarFactory(audiBuilder);

        System.out.println(factory.getBuilder().getCar());

        factory = new CarFactory(BMWBuilder);

        System.out.println(factory.getBuilder().getCar());
    }

}
```

## 总结

### 概述

> 车 -> Product

> AudiBuilder,BMWBuilder -> ConcreteBuilder

> CarFactory -> Director

>造车工厂因为是流水线作业，有固定的零件制造顺序

>不同厂商的制造工艺决定了其产出零件的特性

### 优点

> 将对象的创建过程和对象本身相互隔离,使得细节依赖于抽象,符合依赖倒置原则

### 缺点

> 产品组成属性必须相对固定，如有变化将改变所有建造者实现，违反开闭原则