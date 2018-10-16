# springMVC

## 核心概念

1. aspect 切面

2. join point 连接点

3. target Object 目标对象 织入之前的对象

4. AOP proxy  织入之后产生的代理对象

5. weaving 织入 对目标对象进行功能增强的过程

6. advice 通知 织入代码出现在目标对象的位置称为通知

7. pointcut 切点  join point 的集合 定义了织入的规则

8. springAop与aspectJ区别

   AOP时面向切面编程的思想,springAOP 与AspectJ是两种不同的实现,springAOP使用了AspectJ的风格

## 代理方式

1. jdk动态代理

2. cglib

3. 当aop的目标对象使用类实现的方式作为bean对象时,aop代理方式将会使用cglib,当开启自动代理<aop:aspectJ-autoproxy>有接口时默认使用jdk动态代理若开启class代理则会使用cglib

4. 党对源码进行分析时,在test方法中打断点然后在执行进去,不要直接在源码中打断点,其它程序也有可能会调用该方法,导致中断的位置不正确.

   ## 源码分析

   1. sping在初始化的时候会将所有的对象织入到IOC容器中去 IOC容器本身是一个currentMap集合,通过singletonObjiects.getBeanName()获取对象.
   2. lamda 表达式的实现方式,执行方法时才执行lamda语句
   3. 当使用接口代理方式时,spring 通过initBean方法将原生bean对象的name和接口类型获取到并生成了一个新的代理对象,没有对原生bean对象进行改变
   4. createAopProxy.getProxy()根据传入的tProxyClassLoader选择对应的代理工厂产生代理对象