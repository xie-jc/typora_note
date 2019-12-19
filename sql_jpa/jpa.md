#### 1.JPA简介

(1)jpa:Java Persistence API(java持久层技术)

(2)目的:①简化现有jse和jee开发   ②希望整合orm技术

(3) JPA的总体思想和现有Hibernate、TopLink、JDO等ORM框架大体一致,分为3个部分:①orm元数据映射   ②api接口   ③查询语言

#### 2.jpa基础配置

(1)配置依赖(如hibernate、springdata)

(2)创建jpa配置文件persistence.xml

①在maven项目:resources目录下创建META-INF目录,在该目录下创建persistence.xml

②普通项目:在classpath下创建META-INF目录

(3)创建实体类及映射配置(xml或注解)

​	Ⅰ常用注解

​		①Entity  使jpa扫描,作为持久化类。属性name值可以作为JPQL的表名,默认值为当前类名

​		②Table  映射的表名设置,name属性值为表名

​		③Id  将该属性标识为主键对应字段

​		④GenaretedValue  主键生成策略,属性strategy(GenerationType.[AUTO|IDENTITY|SEQUENCE|TABLE] ),其中auto将生成策略交给数据库厂商选择选择、值为identity时Oracle不支持、值为table会在数据库中建立序列表( 该表有两个字段,第一个字段引用不同关系表,第二个字段是该关系表的最大序号,它会随着数据的插入逐渐累加)、sequence为oracle所支持的序列生成器方式

​		⑤Column  name属性值为列名、length值为字符长度、nullable是否可以为null,例:

```java
@Column(name="login_name",length=20,nullable=null)
```

​		⑥Temporal 对时间类型映射, Temporal.[DATE|TIME|TIMESTAMP],可以贴@Column上

​	ⅡⅢ

(4)EntityManagerFactory对象创建和EntityManager对象获取方法创建



