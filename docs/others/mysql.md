## 创建表

```sql
CREATE TABLE t_message(
	id INT UNSIGNED PRIMARY KEY,
	content VARCHAR(200) NOT NULL,
	type ENUM("公告", "通报", "个人通知") NOT NULL,
	create_time TIMESTAMP NOT NULL,
	INDEX idx_type (type)
);
```


## 查询

### 执行顺序

from > where > group by > select > order by > limit

* 查询数量使用count

  ```sql
  // 查询10和20部门，底薪超过2000， 且工龄超过15年的员工数量。
  SELECT COUNT(*) FROM t_emp
  WHERE deptno IN (10,20) AND sal>=2000
  AND DATEDIFF(NOW(),hiredate)/365 >= 15;
  ```

* where语句不能使用聚合函数。条件不明确。

  ```sql
  SELECT COUNT(*) FROM t_emp
  WHERE hiredate >="1985-01-01"
  AND sal > AVG(sal); // 错误。 wherel
  ```

  

### 分组查询

* 查询语句中如果含有GROUP BY子句， 那么SELECT子句中的内容：可以包含聚合函数，或者GROUP BY子句的分组列，其余内容均不可以出现在select子句中。

  ```sql
  select deptno, COUNT(*), AVG(sal)
  from t_emp group by deptno;
  
  // 错误。deptno 已经是组合后一组数据，那sal是针对哪一个呢。
  select deptno, COUNT(*), AVG(sal), sal
  from t_emp group by deptno;
  ```

  

* 逐级分组

  ```sql
  select deptno, job, count(*), avg(sal)
  from t_emp group by deptno, job
  order by deptno;
  ```

  

#### 对分组结果集再次做汇总计算

```sql
// with rollup 对结果汇总
select deptno, COUNT(*), AVG(sal), MAX(sal), MIN(sal)
from t_emp
group by deptno with rollup;
```

#### GROUP_CONCAT函数

group_concat 函数可以把分组查询中的某个字段拼接成一个字符串。（可以把非分组字段合成一条记录）

```sql
// 查询每个部门内底薪超过2000元的人数和员工姓名（非分组字段）
select deptno,group_concat(ename), count(*)
from t_emp 
where sal >= 2000
group by deptno;
```

#### Having 子句

依赖于group by的条件查询

* where子句中的聚合函数需要确定范围。

```sql
// 查询部门平均底薪超过2000元的部门编号。
select deptno
from t_emp
where AVG(sal)>= 2000 // 错误：针对部门。分组在where之后执行
group by deptno;

// 正确：
select deptno
from t_emp
group by deptno HAVING avg(sal)>=2000;
```

```sql
// 查询每个部门中，1982年以后入职的员工超过2个人的部门编号
se
```



