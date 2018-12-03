# JMM内存模型

## 新生代

### eden（伊甸园）：s1：s2=8:1：1

—Xms开始大小

—Xmx最大大小

—Xmn每次扩展的大小

—XX：+xxx(+代表布尔类型)

—X代表不同的虚拟机有不同的结果

—xx表示虚拟机的版本不同

## 老年代

分配担保

Minor GC之前检查

老年代最大连续空间是否大于新生代所有对象之和

### 永久代（1.8以前）

### metaspace元空间（1.8）

堆外内存，可以无限扩展，直到系统内存不够

## GC

1. GC条件
   1. 判断算法
      - 引用计数
        - 无法解决循环计数的问题
      - 可达性分析
        - GCroot
        - 虚拟机栈本地变量表引用的对象
        - 方法区中
          - 类静态变量引用的对象
          - 常量引用的对象
        - 本地方法栈中JNI引用的对象
      - 不可达的对象如何回收
        - finalize（）方法可以在GC之前拯救一次，但第二次GC时将不再生效（不推荐使用，不保证生效）

   ## 垃圾回收

   ### 内存规整

   指针碰撞

   1. 采用cas方式控制
   2. 使用栈上分配的方式
      1. 每个线程都有一块TLAB（Thread Local Allocation Buffer）
   3. 要求内存规整

   ## Free List（空闲列表）

   ## Minor GC 

   新生代GC方式

   会将eden区和s0区的对象转到s1区

   ## Major GC

   老年代GC方式

   对象进入老年代的条件

   1. 对象很大（ 限定条件-XX：PretenureSizeThreshold=3145728     3M）
   2. 长期存活的对象（最大的MinorGC次数 -XX：MaxTenuringThreshold）
   3. 动态年龄判断：相同年龄所有对象的大小总和》Survivor空间的一半

   ### Full GC

   stw






