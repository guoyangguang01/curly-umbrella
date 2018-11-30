## Tomcat目录结构

**conf**
`catalina.policy`: tomcat安全策略文件,控制jvm相关操作

`catalina.properties` : tomcat catlina 行为控制 

配置文件

catalina : engine引擎的通用配置

`logging.properties`: tomcat日志配置文件,jdk loging

 `server.xml`:   tomcat server 配置文件

- `GlobaNamingResources`: 全局JNDI资源 (java naming directory interface)

`context.xml` :Context 配置文件

`tomcat_user.xml`:tomcat 角色配置文件

`web.xml` : servlet 标准的web.xml部署文件,tomcat 默认实现部分 配置在里面 

**lib目录**
tomcat存放共用类库的位置

#### logs目录

`localhost.${date}.log`:当tomcat 无法启动时,一般看此日志,如类冲突

- `NoClassDefFoundError` 
- `ClassNotFoundException`

`catalina.${date}.log`:控制台输出,`system.out`外置

### webapps目录

简化web应用部署的方式

### 部署web应用

#### 方法一:放置在webapps目录下

#### 方法二:修改 `conf/server.xml` 

添加`context`元素

#### 方法三:配置独立的context.xml文件