---

title: JAVA内存分区
date: 2017-11-29 16:34:22
tags:
	- JAVA

---

## Young

### Eden


1. 所有新创建的对象都在Eden区
2. 当Eden满后会触发minor GC将仍然存货的对象复制到其中一个Survivor


### 2Survivor

1. minor GC后，一个Survivor中存活的对象会复制到另外一个，保证其中一个Survivor始终是空的

## Old

1. Survivor满后触发 minor GC后仍然存活的对象会到Old中,如果Survivor中的对象足够老也会存到Old中
2. 如果Old区满了会触发Full GC，回收整个堆内存

## Perm

1. 存放的主要是类的Class对象，如果一个类被频繁的加载，也可能会导致Perm区满
2. Perm区的垃圾回收也是由Full GC触发的

## 建议

Sun对堆中不同代的大小也给出了建议，一半建议Young区的大小为整个堆的1/4，而Young区中Survivor区一半设置为整个Young区的1/8 