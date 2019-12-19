#### 一、注入方式（3种）

1.内部直接new

2.调用@bean方法

3.贴组件注解，通过@Autowired注入

4.为value时直接通过set方法设置，value等于的是占位符时之后讲

#### 二、多个同类型bean注入冲突

1.@

2.@primary 首选项

3.传入参数名(类似Autowired先找类型，再安bean的引用名)

