①hibernate核心配置文件:hibernate.cfg.xml   ②映射文件:Xxx.hmb.xml

#### 1.hibernate中DML操作

 (1)基本增删改操作

①session.sava(obj)   ②delete(obj)   ③update(obj)   ④saveOrUpdate(obj)

#### 2.hibernate查询

(1)按主键查询 get和load查询
(2)hql查询	

```java
String hql="from 类名";
Query query=session.CreateQuery(hql);//获取hql查询对象:
//设置查询参数
query.setString("","");//用 :xxx 做占位符(推荐等级2)-->当传入多个参数时用map集合
query.setPropertise(map);//(推荐等级3)
query.setParameter(0,obj);//用 ？做占位符-->(推荐等级1)
session.CreateQuery(sql).list();
session.CreateQuery(sql).executeUpdate();//执行更新或者删除操作
```
> 单表查询返回的数据直接封装到List集合中，多表或者其他查询返回Object数组对象或者相关对象存储->返回数据存在于list中第一个元素中，若只有一列数据可用简单或者date类型存储
>

#### 3.对象关系

(1)对象关系

①依赖关系:uses-a,A类依赖B类，缺少依赖B类A类无法编译，A类中调用的B类的方法和属性

②关联关系:has-a，A对象依赖于B对象，且B类被引用为A类的属性，A和B为关联关系(AB处于同一级别)

③聚合关系:has-a，强关联关系(AB为整体和个体，非同一级别)，个体可以离开整体而存在(即当A对象被销毁时，B对象任然可以存在)，A在构造时需要传入B对象

④组合关系: belong-to ,比聚合关系更强的关联关系，B对象的生命周期受A控制

⑤泛化关系:is-a，即继承关系

```java
//依赖、关联、聚合、组合差异化代码对比(java)
class B{                       class Dependency{//调用b方法或属性
    public void method(){};         public void method(){new B().method()}
}                              }
class Assocation{              class Cohesion{//聚合,需传入对象
    private B b;               		private B b;
}                                   public Cohension(B b){
class Combination{    					this.b=b
	private B b; 					}
    public Combination(){      }
    	b=new B();
	}
} //组合,完全掌握B的控制                
```

(2)关联关系

①按导向性分:单向关联、双向关联

②按多重性分

​	一对一：将两表分主表(做成many方)、子表(one方),主表维护子表,存主表；casecade属性需要设置

​	一对多:（many方持有关系，默认many方维护关系->即可以通过many维护one方、稍稍有问题）
​      many-to-one、set中one-to-many
​	多对多:set中manyt-to-many
​		nverse:true让对方维护关系(如外键和中间表)，默认为false->在one方、即对方，多对多随意，谁维护关系就操作谁
​		casecade属性(自动保存/删除关联对象)：all、sava-update、delete、none

#### 4.其他知识

(1)缓存

①默认开启一级缓存,范围在单个会话内不在发重复sql   ②一级缓存测试:关闭缓存session.evict(obj)   ③二级缓存:一般用第三方,还需要在配置文件配置开启二级缓存

(2)整合数据库连接池时，不同连接池属性是不同的