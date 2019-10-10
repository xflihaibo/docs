# my sql

修改密码

```mysql
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'root';
-- 刷新
FLUSH PRIVILEGES;
```

创建 student 表

```mysql
CREATE TABLE student
(
    id INT(11) NOT NULL PRIMARY KEY  auto_increment,
    name VARCHAR(50) NOT NULL,
    age INT(11) DEFAULT NULL,
    city VARCHAR(64) DEFAULT '上海'
)
```

表查询

```mysql
DECS student //查询表结构
SELECT * FROM student //查询表数据
```

列操作

```mysql
-- 增加表里的字段
ALTER TABLE student ADD COLUMN idcard VARCHAR(64) NULL

-- 修改列
ALTER TABLE student MODIFY idcard VARCHAR(128)  NULL

-- 删除列
ALTER TABLE student DROP idcard
```

添加约束

```mysql
-- 添加主建
ALTER TABLE student ADD PRIMARY KEY(id)
-- 添加唯一约束
ALTER TABLE stu ADD UNIQUE INDEX uq_student_idcard (idcard)
-- 增加默认约束
ALTER TABLE stu MODIFY COLUMN age INT(11) DEFAULT 20  
-- 主外键
ALTER TABLE score ADD CONSTRAINT fk_score_stu_id FOREIGN KEY (stu_id) REFERENCES stu(id)
```

```mysql
INSERT INTO student (name, age, city)
VALUES('张三', 20, '上海')


SELECT * FROM student


UPDATE student SET age=40, city='北京' WHERE id=1

UPDATE student SET age=40, city='上海' WHERE id=1 and city='北京'

UPDATE student SET age=60, city='郑州' WHERE id=1 or age=20

-- 删除 不需要提供列名
-- 如果是主表 需要删除子表
-- 会写入目录 可以恢复
DELETE FROM student WHERE id=2

-- 重置标示种子 不写备份 没有日志
TRUNCATE TABLE student




-- 查询

-- 查询 北京同学信息

SELECT id,name
FROM student
WHERE city='北京'
ORDER BY id ASC

-- 查询 别名

SELECT id,name,city AS home  
FROM student
WHERE city='北京'
ORDER BY id ASC

-- age null
SELECT *
FROM student
WHERE age IS NULL

-- 默认常量列

SELECT id,name,'中国' AS country  
FROM student
WHERE city='北京'
ORDER BY id ASC

-- 分页

SELECT id,name,city,'中国' AS country  
FROM student
LIMIT 4,2

//查询数据
SELECT * FROM score WHERE grade BETWEEN 70 AND  100



-- 表查询城市

SELECT DISTINCT city
FROM student

-- + 代表相加 字符转化为 0
SELECT 1+1 -- 2
SELECT 'a'+'b' -- 0
SELECT CONCAT('a','b') -- ab


SELECT  *
FROM student
WHERE name LIKE '李%'
-- WHERE name LIKE '%李%' 李—

-- 链接
SELECT  CONCAT(name,city)
FROM student

-- 链接符号
SELECT  CONCAT_WS('__',name,city)
FROM student
--  FORMAT(X,D) 数字格式化
-- LOWER(str) 转小写字符
-- UPPER(str)转大写字符
-- LEFT(str,len) 返回字符串最左边的字符
-- RIGHT(str,len) 返回字符串最右边的字符
-- LENGTH(str) 取字符长度
-- SUBSTR(str FROM pos FOR len)  截取字符串
-- INSTR(str,substr) 字串在父串的索引
-- TRIM([{BOTH | LEADING | TRAILING} [remstr] FROM] str)去空格
-- LPAD(str,len,padstr) 左补零
-- REPLACE(str,from_str,to_str) 替换

--   数学
-- CEIL(X) 向上取整
-- FLOOR(X) 向下取整
-- DIV  整数取
-- MOD(N,M) 取余数
-- POWER(X,Y) 幂次方运算
-- ROUND(X) 四舍五入
-- TRUNCATE(X,D) 数字截取

--  时间
-- NOW()
-- CURDATE()
-- CURTIME()
-- SELECT DATEDIFF(expr1,expr2) 两个时间差
-- SELECT DATE_ADD(date,INTERVAL expr unit) //时间加

-- SELECT DATABASE() // 数据库名称
-- SELECT VERSION() //mysql 版本
-- SELECT USER() //获取user
-- SELECT LAST_INSERT_ID()
-- SELECT PASSWORD(str) 修改秘密

-- 流程控制
SELECT IF(1>3,1,3)

SELECT CASE grade
    WHEN 100 THEN '满分💯'
    WHEN 90 THEN '优秀'
    ELSE '其他'
  END
    FROM score

SELECT CASE
    WHEN grade = 100 THEN '满分💯'
    WHEN grade >= 90 THEN '优秀'
    ELSE '其他'
  END
    FROM score

-- 自定义函数

set global log_bin_trust_function_creators=TRUE;

SELECT DATE_FORMAT(NOW(),'%Y 年')

CREATE FUNCTION ZNOW() RETURNS VARCHAR(64) RETURN DATE_FORMAT(NOW(),'%Y 年')；

SELECT ZNOW()；

CREATE FUNCTION f1()  RETURNS VARCHAR(30) RETURN DATE_FORMAT(NOW(),'%Y年%m月%d日 %H点:%i分:%s秒');
#执行自定义函数
SELECT f1();

#创建有参函数
CREATE FUNCTION   f2(num1 INT ,num2 INT)  RETURNS FLOAT(10,2) RETURN (num1+num2)/2;
#执行自定义函数
SELECT f2(5,4);


-- 聚合函数 统计数据
SELECT  * from score
// 总分
SELECT SUM(grade) FROM score
SELECT SUM(grade) FROM score where stu_id=1
-- 平均分
SELECT AVG(grade) FROM score where stu_id=1
-- 条数
SELECT COUNT(grade) FROM score where stu_id=1
-- 最大
SELECT MAX(grade) FROM score
-- 最小
SELECT MIN(grade) FROM score


--  分组
SELECT 查询方式
FROM 表名
WHERE 条件
GROUP BY 分组字段
HAVING 分组后的过滤条件
ORDER BY 列名 排序
LIMIT 偏移量 条数


SELECT course_id ,MAX(grade)
FROM score
GROUP BY course_id
ORDER BY MAX(grade) ASC

SELECT *
FROM student
WHERE age>(SELECT AVG(age)FROM student)

//不在范围内
SELECT *
FROM student
WHERE id NOT IN (SELECT student_id FROM score)

SELECT *
FROM student
WHERE EXISTS  (SELECT * FROM score WHERE score.student_id = student.id )

-- 表链接
-- 内链接
SELECT * FROM student INSERT JOIN score ON student.id=score.stu_id
-- 左外链接
SELECT * FROM student LEFT JOIN score ON student.id=score.stu_id
-- 左外链接
SELECT * FROM student RIGHT JOIN score ON student.id=score.stu_id
-- 外链接
SELECT * FROM student OUTER JOIN score ON student.id=score.stu_id
-- 多表链接
SELECT * FROM stu ,score ,course, WHERE score.stu_id=stu.id AND score.course_id=course.id


SELECT * FROM cate
-- 关联产品父子级信息
SELECT * FROM cate c1 INSERT JOIN cate c2 on c1.id=c2.parent.id
-- 关联产品父子级信息
SELECT c1.id COUNT(*) FROM cate c1 INSERT JOIN cate c2 on c1.id=c2.parent.id
WHERE c1.parent_id
GROUP BY  c1.id

-- 删除重复数据 删除
SELECT * FROM cate c1 LEFT JOIN
(SELECT id,name FROM cate GROUP BY name HAVING COUNT(*)>1)c2
ON c1.name =c2.name
WHERE c1.id != c2.id


-- 把 stu城市 插入 新的表里去
INSERT INTO provice(name) SELECT DISTINCT city FROM stu

-- 更新省份

UPDATE student
INSERT JOIN provice on student.city = provice.name
SET student.city=provice.id

-- 修改字段名称
ALTER TABLE stu
CHANGE COLUMN city city_id INT(11) NOT NULL AFTER age;
```

## 事务

完整性 不可分割
一致性
事务之间相互隔离
持久性

```mysql
-- 开启事务
BEGIN
UPDATE account SET balance=balance-10 WHERE id=1
-- 回滚事务
ROLLBACK
UPDATE account SET balance=balance+10 WHERE id=2
-- 提交事务
COMMIT;
```

bluebord
