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

#### 3.关联查询

分类：单向关联、双向关联

(1)一对一：将两表分主表(做成many方)、子表(one方),主表维护子表,存主表；casecade属性需要设置

(1)一对多:（many方持有关系，默认many方维护关系->即可以通过many维护one方、稍稍有问题）
      many-to-one、set中one-to-many
(2)多对多:set中manyt-to-many
inverse:true让对方维护关系(如外键和中间表)，默认为false->在one方、即对方，多对多随意，谁维护关系就操作谁
casecade属性(自动保存/删除关联对象)：all、sava-update、delete、none

#### 4.其他知识

(1)缓存

①默认开启一级缓存,范围在单个会话内不在发重复sql   ②一级缓存测试:关闭缓存session.evict(obj)   ③二级缓存:一般用第三方,还需要在配置文件配置开启二级缓存

(2)整合数据库连接池时，不同连接池属性是不同的