#### 1.自动装配原理

AnnotationConfigApplicationContext(or WebApplicationContext)会创建@EnableAutoConfig-->SpringFactoryLoader-->读取整个项目中META-INF/spring.factories中的XXXAutoConfiguration-->创建对应的bean放在容器中

#### 2.静态资源处理

①默认静态资源目录(resources下的):public、static、resources或者META-INF/resources   ②让自己的目录成为静态资源目录spring.resources.static-location

#### 3.java模板引擎技术（动态资源处理、放在templates目录中）

①jsp(spring-boot支持性较差)、Thymeleaf(spring-boot推荐、但性能差别较大,慎用;优势分离前后端人员操作代码位置)、velocity、freemarker

②freemarker之前配置xml(做两项配置),整合后会自动装配,文件后缀“.ftl”。

③注意:freemarker中默认是无法拿到session中数据,需要自己配置expose-session-attributes为true:其他的request中的也拿不到,但是一般用model传数据了

统一异常处理:

@ControllerAdvice贴类上 @ExceptionHandler(Exception.class或者其他类)贴方法上,方法中常用参数Exception ex、HandlerMethod handlerMethod-->内部可以做handlerMethod.getBean().getClass() 获取错误类名、handlerMethod.getMethod().getName() 获取错误方法名、ex.getMessage() 获取错误信息

异常页面覆盖(resources下的):①静态:public/error/404.html || 500.html || 5xx.html   ②动态:templates/error/404.ftl || ...

springboot注册servlet组件

(1)servlet3.0的标准,①解@WebServlet("/"),类继承HttpServlet   ②Filter贴@WebFilter(urlPartterns="/*"),类实现Filter  ③监听器注册@WebListener,类实现ServletContextListener    ④需要在配置类上tie@ServletComponentScan

(2)springboot提供标准(3.0以下使用):注册一个ServletRegistrationBean/FilterRegistrationBean/ServletListenerRegistrationBean示例

```java
@bean
public ServletRegistrationBean xxxServlet(){
    ServletRegistrationBean bean=new ServletRegistrationBean();
    bean.setServlet(new Xxxservlet());//setXxx根据组件类型
    bean.addUrlMappings("/xxxServlet");//filter为addUrlPatterns("/*");
    return bean;
}
```

文件上传下载:

上传文件时表单类型:enctype="multipart/form-data";springboot默认支持上传,可在配置文件配置pring.multipart.size/

后台处理:定义上传存储路径@Value(“${file.path}”)

参数MultipartFile file 方法内部处理:得到后缀、生成服务器名、FileCopyUtils(file.getInputStream(),new FileOutputStream(new File("存储路径")))

springboot环境下的拦截器:mvc中采用注解+配置文件配置

拦截器类定义:方式一:注解 方式二:继承HandlerIntercepterAdapter  内中覆盖对应方法

配置类继承WebMvcConfigurerAdater   覆盖addInterceptors方法

```java
//配置类继承WebMvcConfigurerAdater  
public void addInterceptors(InterceptorRegistry registry){
    registry.addInterceptor(xxInterceptor()).addUrlPatterns("/*");
}
@Bean 
public XxInterceptor xxInterceptor(){
    return new XxInterceptor();
}
```

