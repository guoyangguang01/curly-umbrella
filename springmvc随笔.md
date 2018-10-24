socket 长连接 http短连接

有状态 无状态

springmc

controller实现的三种方式

1. 实现controller的handlerRequest方法
2. xml
3. 注解

springmvc流程

DispatcherServlet根据实现controller方式的不同通过handlerMapping处理器获取不同的handler处理器对象HandlerExcutionChain执行链责任链模式

1. 首先在DispatcherServlet类中通过getHandler方法获取HandlerExcutionChain对象,其过程为:
   1. 遍历HandlerMappings,获取与当前实现方式所匹配的HandlerMapping,xml配置方式会拿到BeanNameUrlHandlerMapping,
   2. 使用注解方式会拿到RequestMappingHandlerMapping
   3. 得到MapperHandler对象
2. HandlerAdapter通过拿到的Handler对象适配到正确的执行流程,执行对应的处理
   1. xml会使用Simple
   2. 注解配置会使用RequestMappingHandlerAdapter适配器
3. mapperHandler执行applyPreHandler方法进行拦截操作
4. xml方式将handler强转成为controller执行方法得到ModelAndView对象
5. 注解方式通过执行invokeHandlerMethod得到ModelAndView对象
6. 通过视图解析器ViewResolver将物理视图转化为到逻辑视图对象
7. 渲染视图,返回请求;