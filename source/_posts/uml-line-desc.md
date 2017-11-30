---
title: uml类图简要说明
date: 2017-11-29 16:50:18
tags:
	- UML

---

## UML类图说明

### 继承

![](https://ws1.sinaimg.cn/large/9aaab0cfgy1flwmmldfihj202a04qjr9.jpg)```
classB extends classA{}
```

---### 实现

![](https://ws1.sinaimg.cn/large/9aaab0cfgy1flwmosz6tsj202h04qmx1.jpg) 

```
classD implements classC{}
```
---

### 依赖
![](https://ws1.sinaimg.cn/large/9aaab0cfgy1flwms84jkyj202k04qa9x.jpg)

```
classF{
	method(ClassE classE);
}
```
---

### 关联
![](https://ws1.sinaimg.cn/large/9aaab0cfgy1flwmuz663tj202d04pa9x.jpg)

```
classH{
	ClassG classG;
}
```
---

### 聚合

![](https://ws1.sinaimg.cn/large/9aaab0cfgy1flwmwja183j202604oa9x.jpg)

```
classJ{
	ClassI classI;
}
```

classJ has classI, 公司拥有员工的关系，生命周期不在一起，和关联在类的表达上一致，只是强化了拥有关系

---

### 组合

![](https://ws1.sinaimg.cn/large/9aaab0cfgy1flwmzb3k5ij202504ldfp.jpg)

```
classL{
	ClassK classK;
}
```

classL contains classK, 强聚合关系，生命周期完全一致
