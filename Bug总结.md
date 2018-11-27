# Bug总结

1. **现象**:控制台疯狂打印日志,无法创建DataSource属性和sqlsessionFactory对象,所有的mapper对象都无法创建

   **问题解决**:最后发现dao未导入springframework.jdbc的jar包 

2. **现象**:dubbo找不到服务提供者 NO Provider

   问题:service没有添加service注解

   解析:dubbo生产者或提供者错误,一般需要找service,消费者错误一般找controller

3. **现象**:前端发送的对象后端接收到的是null

   问题:没有加ReponseBody注解

   **解析**:springmvc将前端的json数据转化为pojo对象时需要加ResponseBody注解进行匹配

4.**现象**:Could not resolve placeholder 

**问题**: Spring容器采用反射扫描的发现机制，在探测到Spring容器中有一个org.springframework.beans.factory.config.PropertyPlaceholderConfigurer的Bean就会停止对剩余PropertyPlaceholderConfigurer的扫描（Spring 3.1已经使用PropertySourcesPlaceholderConfigurer替代PropertyPlaceholderConfigurer了）。

而<context:property-placeholder/>这个基于命名空间的配置，其实内部就是创建一个PropertyPlaceholderConfigurer Bean而已。换句话说，即Spring容器仅允许最多定义一个PropertyPlaceholderConfigurer(或<context:property-placeholder/>)，其余的会被Spring忽略掉。

解决方法就是改成<context:property-placeholder location="classpath:redis.properties" ignore-unresolvable="true"/>即可！

5. 现象:Could not find key 'spring.liveBeansView.mbeanDomain' in any property source

   问题:没有为类添加Component注解,无法被扫描到
