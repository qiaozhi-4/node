

#### 查询某段时间的数据

```sql
/*查询大于这个时间节点的所有数据*/
SELECT * FROM table_name c WHERE c.ACCEPTDATE > to_date('2015/5/15 10:00:00','yyyy/mm/dd hh24:mi:ss');

/*查询小于这个时间节点的所有数据*/
SELECT *FROMtable_name cWHERE c.ACCEPTDATE < to_date('2015/5/15 10:00:00','yyyy/mm/dd hh24:mi:ss');

/*查询这两个时间节点之间的所有数据*/
SELECT *FROM table_name c WHERE c.ACCEPTDATE BETWEEN to_date('2019/12/17 04:00:00','yyyy/mm/dd hh24:mi:ss')  AND to_date('2019/12/17 11:00:00','yyyy/mm/dd hh24:mi:ss');
```

------------------------------



#### 临时表语法

```sql
with 给表起名 as(
.....查询语句
)select * from 开始起的名字
```

--------------------



#### 获取年/月/日/时/分/秒

```sql
-- 可以随意组合使用
-- 年
to_char(sysdate,'YYYY')
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

----------------------



#### 合并两个集合（查询）

 **Union：对两个结果集进行并集操作，不包括重复行，同时进行默认规则的排序；** 

UNION在进行表链接后会筛选掉重复的记录，所以在表链接后会对所产生的结果集进行排序运算，删除重复的记录再返回结果。
实际大部分应用中是不会产生重复的记录，最常见的是过程表与历史表UNION

 **Union All：对两个结果集进行并集操作，包括重复行，不进行排序；** 

 如果返回的两个结果集中有重复的数据，那么返回的结果集就会包含重复的数据了。 

----------------------





#### 类型转换

###### 字符串，时间相互转换

```sql
--字符串转时间
select to_date('20210908', 'yyyymmdd') from dual
select to_date('2021-9-8 11:21:55', 'yyyyfm-mm-dd hh24:mi:ss') from dual

--时间转字符串
select to_char(sysdate, 'yyyy/mm/dd')  from dual
```

-------------------



###### 转数字类型

```sql
select to_number('123') from dual
```

----------------





#### Oracle计算时间差函数

注意事项：开始时间和结束时间一定要转换为 date 类型

```sql
--天
ROUND(TO_NUMBER(END_DATE - START_DATE))
--年
ROUND(TO_NUMBER(END_DATE - START_DATE))/365
```

----------------





#### oracle 向上取整、向下取整

###### ceil函数实现向上取整

```sql
SELECT CEIL(10.12) FROM DUAL ; --返回11
SELECT CEIL(10.99) FROM DUAL ; --返回11
SELECT  CEIL(2.222*100)/100 FROM DUAL ; --返回2.23
```

----------------



###### floor、trunc实现向下取整

```sql
SELECT FLOOR(10.12) FROM DUAL; --返回10
SELECT FLOOR(10.99) FROM DUAL;--返回10

SELECT TRUNC(10.12,0) FROM DUAL ;--返回10，第二个参数表示保留小数的位数，可以不写，默认为不保留小数
SELECT TRUNC(10.99,0) FROM DUAL ;--返回10
```

----------------



###### round实现四舍五入取整

```sql
SELECT ROUND(10.12) FROM DUAL ;--返回10
SELECT ROUND(10.99) FROM DUAL; --返回11
```

----------------







#### oracle 使用正则表达式

###### REGEXP_LIKE ：

与LIKE的功能相似，可以支持按正则表达式与文本进行匹配

```sql
REGEXP_LIKE(STRING, REGEX, MODIFIER)
```

**STRING**：需要进行正则处理的字符串
**REGEX**：进行匹配的正则表达式
**MODIFIER**：模式（‘i’不区分大小写进行检索；‘c’区分大小写进行检索。默认为’c’）

```sql
SELECT ENAME, JOB FROM EMP WHERE REGEXP_LIKE(JOB, '(clerk|analyst)', 'i');
```

----------------



###### REGEXP_INSTR ：

返回指定字符串中与正则表达式匹配部分第一次出现的位置

```sql
REGEXP_INSTR(STRING, REGEX[, START_POSITION[, OCCURRENCE[, RETURN_OPTION[, MODIFIER]]]])
```

**STRING**：需要进行正则处理的字符串
**REGEX**：进行匹配的正则表达式
**START_POSITION**：起始位置，从字符串的第几个字符开始正则表达式匹配（默认从第一个字符开始，值为1）
**OCCURRENCE**：获取分割出来的第几组子串（分割后最初的字符串会按分割的顺序排列成数组）
**RETURN_OPTION**：指定返回值的类型。为0，则返回匹配值第一次出现的第一个字符的角标，非0，则返回匹配值第一次出现的最后一个字符的角标+1
**MODIFIER**：模式
‘c’ 区分大小写进行检索。默认为‘c’
‘i’ 不区分大小写进行检索
‘n’ 允许句点(.)作为通配符去匹配换行符。如果省略该参数，句点将不匹配换行符
‘m’ 将源串视为多行。即 Oracle 中将^和$分别看作源串中任意位置任何行的开始和结束，而不是仅仅看作整个源串的开始或结束。如果省略该参数，则Oracle将源串看作一行。
‘x’ 忽略源串中的空格字符。默认情况下，空格字符与自身相匹配。
返回值：返回满足正则表达式的字符或字符串第一次出现的角标，如果没有找到结果，则返回0

```sql
SELECT REGEXP_INSTR('11a22A33a', 'a') AS STR FROM DUAL;--结果：3
```

------------------------------



###### REGEXP_COUNT ：

返回指定字符串中与正则表达式匹配部分出现的次数

```sql
REGEXP_COUNT(STRING, REGEX[, START_POSITION[, MODIFIER]])
```

**STRING**：需要进行正则处理的字符串
**REGEX**：进行匹配的正则表达式
**START_POSITION**：起始位置，从字符串的第几个字符开始正则表达式匹配（默认从第一个字符开始，值为1）
**MODIFIER**：模式
‘c’ 区分大小写进行检索。默认为‘c’
‘i’ 不区分大小写进行检索
‘n’ 允许句点(.)作为通配符去匹配换行符。如果省略该参数，句点将不匹配换行符
‘m’ 将源串视为多行。即 Oracle 中将^和$分别看作源串中任意位置任何行的开始和结束，而不是仅仅看作整个源串的开始或结束。如果省略该参数，则Oracle将源串看作一行。
‘x’ 忽略源串中的空格字符。默认情况下，空格字符与自身相匹配。
返回值：返回满足正则表达式的字符或字符串出现的次数。

```sql
SELECT REGEXP_COUNT('11a22A33a11a22A33a', '2A', 1, 'c') AS STR FROM DUAL;--结果：2
```

------------



###### REGEXP_SUBSTR ：

截取指定字符串中与正则表达式匹配的部分

```sql
REGEXP_SUBSTR(STRING, REGEX[, START_POSITION[, OCCURRENCE[, MODIFIER]]])
```

**STRING**：需要进行正则处理的字符串
**REGEX**：进行匹配的正则表达式
**START_POSITION**：起始位置，从字符串的第几个字符开始正则表达式匹配（默认从第一个字符开始，值为1）
**OCCURRENCE**：获取分割出来的第几组子串（分割后最初的字符串会按分割的顺序排列成数组）
**MODIFIER**：模式
‘c’ 区分大小写进行检索。默认为‘c’
‘i’ 不区分大小写进行检索
‘n’ 允许句点(.)作为通配符去匹配换行符。如果省略该参数，句点将不匹配换行符
‘m’ 将源串视为多行。即 Oracle 中将^和$分别看作源串中任意位置任何行的开始和结束，而不是仅仅看作整个源串的开始或结束。如果省略该参数，则Oracle将源串看作一行。
‘x’ 忽略源串中的空格字符。默认情况下，空格字符与自身相匹配。

```sql
SELECT REGEXP_SUBSTR('11a22A33a', '[^A]+', 1, 1, 'i') AS STR FROM DUAL;---结果：11
SELECT REGEXP_SUBSTR('11a22A33a', '[^A]+', 1, 1, 'c') AS STR FROM DUAL;--结果：11a22
```

----------------



###### REGEXP_REPLACE ：

替换指定字符串中与正则表达式匹配的部分

```sql
REGEXP_REPLACE(STRING, REGEX, REPLACE_STRING)
```

**STRING**：需要进行正则处理的字符串
**REGEX**：进行匹配的正则表达式
**REPLACE_STRING**：要替换成的字符串 

```sql
SELECT REGEXP_REPLACE('11a22A33a', 'a', '') AS STR FROM DUAL;--结果：1122A33
```

-----------------





#### NVL - 值为 null 则使用默认

 NVL(Expr1,Expr2) 如果Expr1为NULL，返回Expr2的值，否则返回Expr1的值 

```sql
select  NVL(SUM(t.money) ,0)  from Money t
```

---------





#### CASE WHEN

###### SELECT CASE WHEN 用法

```sql
case sex
when '1' then '男'
when '2' then '女'
else '其它'
end;

case 
when sex='1' then '男'
when sex='2' then '女'
else '其它'
end;
```

------------------------



###### **WHERE CASE WHEN 用法**

```sql
SELECT T2.*, T1.*   FROM T1, T2  
WHERE 
(CASE WHEN T2.COMPARE_TYPE = 'A' AND T1.SOME_TYPE LIKE 'NOTHING%' THEN 1               WHEN T2.COMPARE_TYPE != 'A' AND T1.SOME_TYPE NOT LIKE 'NOTHING%' THEN 1               ELSE 0 END) = 1
```

---------------------------------







#### REPLACE 替换指定字符串子串

```sql
REPLACE('字符串','要匹配的子串','要替换成什么')
REPLACE('你好,乔治','乔治','汤姆') --你好,汤姆
REPLACE('你好,乔治;乔治你好','乔治','汤姆') --你好,汤姆;汤姆你好
```



