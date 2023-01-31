#### 查询某段时间的数据

```sql
/*查询大于这个时间节点的所有数据*/
SELECT * FROM table_name c WHERE c.ACCEPTDATE > to_date('2015/5/15 10:00:00','yyyy/mm/dd hh24:mi:ss');

/*查询小于这个时间节点的所有数据*/
SELECT *FROMtable_name cWHERE c.ACCEPTDATE < to_date('2015/5/15 10:00:00','yyyy/mm/dd hh24:mi:ss');

/*查询这两个时间节点之间的所有数据*/
SELECT *FROM table_name c WHERE c.ACCEPTDATE BETWEEN to_date('2019/12/17 04:00:00','yyyy/mm/dd hh24:mi:ss')  AND to_date('2019/12/17 11:00:00','yyyy/mm/dd hh24:mi:ss');
```



#### 临时表语法

```sql
with 给表起名 as(
.....查询语句
)select * from 开始起的名字
```



#### 获取年/月/日/时/分/秒

```sql
-- 可以随意组合使用
-- 年
to_char(sysdate,'yyyy')
-- 月
to_char(sysdate,'MM')
-- 日
to_char(sysdate,'DD')
-- 时
to_char(sysdate,'HH24')
-- 分
to_char(sysdate,'MI')
-- 秒
to_char(sysdate,'SS')
```



#### 合并两个集合（查询）

 **Union：对两个结果集进行并集操作，不包括重复行，同时进行默认规则的排序；** 

UNION在进行表链接后会筛选掉重复的记录，所以在表链接后会对所产生的结果集进行排序运算，删除重复的记录再返回结果。
实际大部分应用中是不会产生重复的记录，最常见的是过程表与历史表UNION

 **Union All：对两个结果集进行并集操作，包括重复行，不进行排序；** 

 如果返回的两个结果集中有重复的数据，那么返回的结果集就会包含重复的数据了。 



