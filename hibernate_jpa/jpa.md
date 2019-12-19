#### 1.JPA简介

(1)jpa:Java Persistence API(java持久层技术)

(2)目的:①简化现有jse和jee开发   ②希望整合orm技术

(3) JPA的总体思想和现有Hibernate、TopLink、JDO等ORM框架大体一致,分为3个部分:①orm元数据映射   ②api接口   ③查询语言

#### 2.简单jpa案例

(1)配置依赖(如hibernate、springdata)

(2)创建jpa配置文件persistence.xml

①在maven项目:resources目录下创建META-INF目录(普通项目在classpath下创建),在该目录下创建persistence.xml,示例:



(3)创建实体类及映射配置(xml或注解)

(4)EntityManagerFactory对象创建和EntityManager对象获取方法创建



