## MyBatis配置方式

1. xml方式 

   通过generator生成器生成Mapper和xml映射文件,使用的时候通过mapper进行操作

   如果搜索的关键字为主键的话,通常都会有方法可以直接操作,如果需要添加其他的条件的话,一般的操作步骤如下:

   1. 创建一个对应的eample对象
   2. example创建一个Critical条件
   3. 在条件上附加方法(query,update,delete.etc)以及参数
   4. mapper对象执行对应的方法,将mapper对象作为参数

2. 注解方式

   需要在xml中开启注解配置或者创建Configeration类,在类中添加相关配置

   注解方式的步骤为:

   1. 在dao层创建相应的dao接口
   2. 为每一个sql添加一个查询的接口
   3. 在接口上添加对应的注解,并在其中添加sql语句

   当同时存在xml和注解配置时,mybatis会首先加载xml配置执行loadXmlResource()方法,在对注解进行检索,进行加载注解配置,因此同样的配置,注解会覆盖xml配置,不同的配置可以共同使用

   ## 批处理

   1. for循环 性能差
   2. foreach 性能高 SQL长度有限制
   3. batch操作 需要自定义session,不适用默认的simpleSession,自己创建batchSession.

   ## 分页

   1. 自定义分页参数
   2. 使用pageHelper分页插件 当查询量大时有性能问题,会使用count(0)计算总页数

   ## 联合查询

   1. resultMap和resultType

   2. association和collection

   3. 查询方式

      1. 嵌套查询

         通过分布查询来实现联合查询

      2. 嵌套结果

   4. N+1问题

      一对多时部分联合查询一个属性会将其联合类的嵌套的其它类一起查询出来

      需要采用懒加载机制来预防这个问题
