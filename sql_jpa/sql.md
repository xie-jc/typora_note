#### 1.存储过程创建

```sql
create [or replace] procedure 
	过程名称(参数1 in|out 参数类型,参数2 in|out 参数类型)
  is | as
  -- 变量声明 
begin
-- 业务 
end;

--(1): 调用方法:
call 过程名称(参数);
--(2): plsql中使用: 
begin
 过程名称(参数);
end;  
```

#### 2.函数创建

```sql
create [or replace] function
    函数名称(参数1  参数类型) return 返回类型
  is
    返回变量 变量类型
  begin
    ...
    return 返回变量
  end;
```

#### 3.jdbc中函数和存储过程调用

(1)调用sql字符串

① "{?=call 方法名(?,?,?)}";
②"{call 方法名(?,?,?)}";

(2)示例

```java
CallableStatement callableStatement =connection.prepareCall(sql);//①语句对象：
callableStatement.setInt(2, 7521);//②设置in参数
callableStatement.registerOutParameter(3, oracle.jdbc.OracleTypes.VARCHAR);//设置out、return类型
callableStatement.execute();//③执行语句
callableStatement.getDouble(1);//④获取out数据
```

