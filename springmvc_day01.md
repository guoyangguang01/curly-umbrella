# 内容介绍

## springmvc介绍（了解）

## springmvc入门（掌握  重点）

## springmvc参数绑定（掌握 重点 ）

## springmvc注解（了解）

------







# 一、springmvc介绍  

## 1､三层架构和mvc模型



1､ 服务端分为哪三层？ 分别使用什么框架？

​	

​	表现层  springmvc  

​        业务层  spring

​	持久层  mybatis



2､  什么是mvc? 



​	model      业务层返回的实体类

​	view         jsp

​	controller   servlet 



## 2､springmvc介绍？



1､什么是springmvc？

​	springmvc是一个表现层的框架，使用了mvc设计模型。



2､为什么要使用springmvc?

​	好用

​	安全



# 二、springmvc入门

## 3､入门需求



点击链接

​		index.jsp ————>  编写后台处理请求，并跳到成功页面。



## 4､环境塔建



第一步：建工程 （添加属性）   

![1538922478843](Z:\Desktop\assets\1538922478843.png)

第二步：建 java 、 resources文件夹 ，并且奶一口

![1538927695814](Z:\Desktop\assets\1538927695814.png)

第三步：导jar包 pom.xml

```xml
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <maven.compiler.source>1.8</maven.compiler.source>
    <maven.compiler.target>1.8</maven.compiler.target>
    <spring.version>5.0.2.RELEASE</spring.version>
  </properties>

  <dependencies>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context</artifactId>
      <version>${spring.version}</version>
    </dependency>

    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-web</artifactId>
      <version>${spring.version}</version>
    </dependency>

    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-webmvc</artifactId>
      <version>${spring.version}</version>
    </dependency>

    <dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>servlet-api</artifactId>
      <version>2.5</version>
      <scope>provided</scope>
    </dependency>

    <dependency>
      <groupId>javax.servlet.jsp</groupId>
      <artifactId>jsp-api</artifactId>
      <version>2.0</version>
      <scope>provided</scope>
    </dependency>

  </dependencies>
```



第四步：web.xml中配置前端控制器

```xml
  <!--配置前端控制器-->
  <servlet>
    <servlet-name>dispatcherServlet</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    <load-on-startup>1</load-on-startup>
  </servlet>
  <servlet-mapping>
    <servlet-name>dispatcherServlet</servlet-name>
    <url-pattern>/</url-pattern>
  </servlet-mapping>
```



第五步：创建springmvc.xml配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/mvc
        http://www.springframework.org/schema/mvc/spring-mvc.xsd
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context.xsd">



</beans>
```



## 5､ 入门实现

第一步：编写index.jsp 

```html
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
    <h3>入门程序</h3>
    <a href="hello">入门程序</a>
</body>
</html>
```



第二步：编写HelloController

```java

public class HelloController {

    public String sayHello(){
        System.out.println("Hello StringMVC");
        return "success";
    }

}
```



第三步:   为HelloController添加注解

```java
// 控制器类
@Controller
public class HelloController {

    /**
     * 入门案例
     * @return
     */
    @RequestMapping(path="/hello")
    public String sayHello(){
        System.out.println("Hello StringMVC");
        return "success";
    }
    

}
```



第四步：springmvc.xml扫描controller ，并吧springmvc传给前端控制器加载。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/mvc
        http://www.springframework.org/schema/mvc/spring-mvc.xsd
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context.xsd">

    <!-- 开启注解扫描 -->
    <context:component-scan base-package="cn.itcast"/>


</beans>
```

web.xml 中配置springmvc.xml

```xml
  <!--配置前端控制器-->
  <servlet>
    <servlet-name>dispatcherServlet</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    <init-param>
      <param-name>contextConfigLocation</param-name>
      <param-value>classpath:springmvc.xml</param-value>
    </init-param>
    <load-on-startup>1</load-on-startup>
  </servlet>
  <servlet-mapping>
    <servlet-name>dispatcherServlet</servlet-name>
    <url-pattern>/</url-pattern>
  </servlet-mapping>
```



第五步：返回 success ，配置视图解析器，和注解驱动。

springmvc.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/mvc
        http://www.springframework.org/schema/mvc/spring-mvc.xsd
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context.xsd">

    <!-- 开启注解扫描 -->
    <context:component-scan base-package="cn.itcast"/>

    <!-- 视图解析器对象 -->
    <bean id="internalResourceViewResolver" class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="prefix" value="/WEB-INF/pages/"/>
        <property name="suffix" value=".jsp"/>
    </bean>


    <!-- 开启SpringMVC框架注解的支持 -->
    <mvc:annotation-driven />

</beans>
```



6､ 执行流程



第一步：服务器启动

 *   创建DispatchServlet
 *   加载springmvc.xml，创建Controller
 *   创建视图解析器
 *   创建注解驱动



第二步：发起请求，处理后跳转

index.jsp ——>. dispatcherServlet ——> helloController——> 视图解析器————> success.jsp





## 6､springmvc组件



* 有哪些组件？

    1､ 视图解析器

    2､ 映射器

    3､ 适配器

* 怎么配置？ 不配置三大件可以吗？

  ```xml
  <!-- 视图解析器对象 -->
  <bean id="internalResourceViewResolver" 		class="org.springframework.web.servlet.view.InternalResourceViewResolver">
      <property name="prefix" value="/WEB-INF/pages/"/>
      <property name="suffix" value=".jsp"/>
  </bean>
  
  
  <!-- 开启SpringMVC框架注解的支持 -->
  <mvc:annotation-driven />
  ```


## 7､requestMapping注解

写在方法

```java
@RequestMapping(path="/hello")
public String sayHello(){
    System.out.println("Hello StringMVC");
    return "success";
}
```

写在类上

```java
@RequestMapping(path="/user")
public class HelloController {
}
```

## 8､requestMapping注解的属性

```java
@RequestMapping(value="/testRequestMapping",params = {"username=heihei"},headers = {"Accept"},method = RequestMethod.GET)
public String testRequestMapping(){
    System.out.println("测试RequestMapping注解...");
    return "success";
}
```

1､ path / value   ： 指定请求的url地址

2､ method  ： 限定请求的方式  

3､ params :  限定请求中必需要有指定的参数

4､ headers：限定请求中必需有指定请求头



面试题 ：http协议请求方式有几种？分别是什么？

8种

get

post

put

delete



head

trace

options

connect



# 三、springmvc参数绑定

##  9､参数绑定入门

1､什么是参数绑定？

2､基本类型的参数绑定有什么要求？

页面

```html
<a href="param/testParam?username=hehe&password=123">请求参数绑定</a>
```

后台

```java
    @RequestMapping("/testParam")
    public String testParam(String username,String password){
        System.out.println("执行了...");
        System.out.println("用户名："+username);
        System.out.println("密码："+password);
        return "success";
    }
```



## 10､对象类型参数绑定



1､  什么是对象类型的参数绑定？

2､ 对象类型的参数绑定有什么要求？

页面

```html
<form action="param/saveAccount" method="post">
               姓名：<input type="text" name="username" /><br/>
               密码：<input type="text" name="password" /><br/>
               金额：<input type="text" name="money" /><br/>
               <input type="submit" value="提交" />
</form>
```



后台

```java
    /**
     * 请求参数绑定把数据封装到JavaBean的类中
     * @return
     */
    @RequestMapping("/saveAccount")
    public String saveAccount(Account account){
        System.out.println("执行了...");
        System.out.println(account);
        return "success";
    }
```



3､ 如果一个对象的属性又是一个对象怎样完成参数绑定？

前台

```html
 <form action="param/saveAccount" method="post">
               姓名：<input type="text" name="username" /><br/>
               密码：<input type="text" name="password" /><br/>
               金额：<input type="text" name="money" /><br/>
               用户姓名：<input type="text" name="user.uname" /><br/>
               用户年龄：<input type="text" name="user.age" /><br/>
               <input type="submit" value="提交" />
 </form>
```



后台

```java
    @RequestMapping("/saveAccount")
    public String saveAccount(Account account){
        System.out.println("执行了...");
        System.out.println(account);
        return "success";
    }
```

```java
public class Account implements Serializable{

    private String username;
    private String password;
    private Double money;

    private User user;
}
```



## 11､乱码解决



- 配置过滤器 web.xml

  ```xml
  <!--配置解决中文乱码的过滤器-->
    <filter>
      <filter-name>characterEncodingFilter</filter-name>
      <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
      <init-param>
        <param-name>encoding</param-name>
        <param-value>UTF-8</param-value>
      </init-param>
    </filter>
    <filter-mapping>
      <filter-name>characterEncodingFilter</filter-name>
      <url-pattern>/*</url-pattern>
    </filter-mapping>
  ```



## 12､集合类型参数绑定（选学）

* list
* map



## 13､日期类型转换异常演示

前台  

```java
    <form action="param/saveUser" method="post">
        用户姓名：<input type="text" name="uname" /><br/>
        用户年龄：<input type="text" name="age" /><br/>
        用户生日：<input type="text" name="date" /><br/>
        <input type="submit" value="提交" />
    </form>
```

后台

```java
    @RequestMapping("/saveUser")
    public String saveUser(User user){
        System.out.println("执行了...");
        System.out.println(user);
        return "success";
    }
```





## 14､编写自定义的类型转换器、配置



1､编写自定义的转换器

```java
/**
 * 把字符串转换日期
 */
public class StringToDateConverter implements Converter<String,Date>{

    /**
     * String source    传入进来字符串
     * @param source
     * @return
     */
    public Date convert(String source) {
        // 判断
        if(source == null){
            throw new RuntimeException("请您传入数据");
        }
        DateFormat df = new SimpleDateFormat("yyyy-MM-dd");

        try {
            // 把字符串转换日期
            return df.parse(source);
        } catch (Exception e) {
            throw new RuntimeException("数据类型转换出现错误");
        }
    }

}
```



2､配置转换器  springmvc.xml

```xml
<!--配置自定义类型转换器-->
<bean id="conversionService" class="org.springframework.context.support.ConversionServiceFactoryBean">
    <property name="converters">
        <set>
            <bean class="cn.itcast.utils.StringToDateConverter"/>
        </set>
    </property>
</bean>


<!-- 开启SpringMVC框架注解的支持 -->
<mvc:annotation-driven conversion-service="conversionService"/>
```



## 16､获取原生servlet api

```java
    /**
     * 原生的API
     * @return
     */
    @RequestMapping("/testServlet")
    public String testServlet(HttpServletRequest request, HttpServletResponse response){
        System.out.println("执行了...");
        System.out.println(request);

        HttpSession session = request.getSession();
        System.out.println(session);

        ServletContext servletContext = session.getServletContext();
        System.out.println(servletContext);

        System.out.println(response);
        return "success";
    }
```





# 四､注解（了解）

1､  @RequestParam  参数名不一致，手动映射。

2､  @RequestBody 获取请求体类内，对get无效。 

3､  @PathVariable 实现restfull风格url





-------->以下为选学

4､  @HidentHttpMethodFilter 

5､  @RequestHeader 获取请求头的值

6､  @CookieValue 获取cookie的值

7､   @ModelAttribute 写在方法上，返回值会传给controller方法、map参数可以传给controller方法

