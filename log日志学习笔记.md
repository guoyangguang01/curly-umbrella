## spring log 学习笔记
1. jcl 循环查找选取log log4J --> jul 
2. jul java 原生日志实现
3. spring jcl 改写了jcl 源码实现,剔除了log4j log4j2 --> slf4j -->else slf4j -->jul
4. 要想在spring中使用log4j实现日志,需要去掉spring的jcl依赖,改用原生jcl,同时添加log4j依赖
5. spring5 使用spring jcl spring4使用jcl
6. process on 在线画图工具
7. slf4j 与 jcl类似,本身不提供具体的日志实现,而是兼容了各类日志实现,通过绑定器(桥接器)来绑定具体的日志