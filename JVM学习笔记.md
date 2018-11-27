# JVM学习笔记

## 程序计数器

记录正在执行的虚拟机字节码指令的地址，当执行native方法时，计数器的值为空（undefined）

每一个线程都拥有独立的程序计数器

## 虚拟机栈

线程私有，每个线程拥有独立的虚拟机栈，拥有线程相同的生命周期

### 栈帧 

存储局部变量表 操作数栈 动态链接 方法出口等信息，每一个方法的完整执行过程都是一个栈帧从虚拟机栈进栈到出栈的过程

### 局部变量表

存储编译器可知的所有基本数据类型，对象的引用和指向字节码指令地址的returnAddress类型

线程请求的深度大于虚拟机所允许的深度将会抛出StackOverflowError，若虚拟机栈可以动态扩展，如果扩展时无法获取到足够的内存，将会抛出OutOfMermoryError异常

### 动态链接

实现运行时多态的关键，运行时确定对象的类型

### 出口

方法正常或异常执行之后的返回的位置

## 本地方法栈

为Native本地方法服务

## JAVA 堆

堆是所有线程共享的，在虚拟机启动是创建的

堆用于存储对象的实例信息，是GC工作的主要区域

动态扩展（由 -xms   -xmx控制）

## 方法区

与堆一样，是所有线程共用的内存区域，用于存储已被虚拟机加载的类型信息，常量（1.7），静态变量，及时编译器编译后的代码（JIT）等数据

方法区未能满足内存需求时，会抛出OutOfMermory异常

### 运行时常量池

存储编译期产生的**字面量**和符号引用

可以存储运行时产生的常量

## 直接内存



![1540732426498](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1540732426498.png)



![1540732520399](D:\Documents\GitHub\curly-umbrella\assets\1540732520399.png)![1540732928402](D:\Documents\GitHub\curly-umbrella\assets\1540732928402.png)

## 

## 垃圾回收算法

### 对象存活判定

1. 引用计数算法

2. 可达性分析算法

   ![1540734528697](D:\Documents\GitHub\curly-umbrella\assets\1540734528697.png)

### 对象引用关系

![1540733871621](D:\Documents\GitHub\curly-umbrella\assets\1540733871621.png)

## 垃圾回收算法

### 标记清除算法（mark-sweep）

![1540734861368](D:\Documents\GitHub\curly-umbrella\assets\1540734861368.png)

### 复制算法（copy）

![1540734891239](D:\Documents\GitHub\curly-umbrella\assets\1540734891239.png)

### 分配担保机制

### 标记整理算法（mark-compact）

![1540734953224](D:\Documents\GitHub\curly-umbrella\assets\1540734953224.png)

### 分代收集算法

