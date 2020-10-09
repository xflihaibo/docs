# my sql

修改密码

```mysql

# yum install mysql
# yum install mariadb-server  //如果已安装可以省略
# systemctl start mariadb.service //启动服务
# systemctl enable mariadb.service //开机启动服务
# mysql -u root -p //登录mysql

mysql -uroot -proot //链接数据库
exit 推出
select Host,User,Password from mysql.user; 查询用户

show datausebases; 查看数据库
use  stu 切换数据库
show tables; 查看数据库中的表
select database(); 查看当前数据库

ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'root'; 修改密码
update user set password=password("123456")where user='root'; // 修改密码
set password for root@localhost = password('123456'); 设置密码

//mysql数据库中的user的表中没有权限
select Host, User,Password from user;
update user set Host='%' where User='root';
flush privileges;

-- 刷新lasrt
FLUSH PRIVILEGES;
mysql -uroot -p123456 ：登陆数据
1.在Linux，先进入/etc，修改my.cnf,任意一行加上"skip-grant-tables"。
2.重启MySQL：systemctl restart mariadb
mysqladmin -uroot -p密码 password 新密码
```

### 创建 student 表

```mysql
CREATE TABLE student
(
    id INT(11) NOT NULL PRIMARY KEY  auto_increment,
    name VARCHAR(50) NOT NULL,
    age INT(11) DEFAULT NULL,
    city VARCHAR(64) DEFAULT '上海'
)
```

### 表查询

```mysql
DECS student //查询表结构
SELECT * FROM student //查询表数据
```

### 列操作

```mysql
-- 增加表里的字段
ALTER TABLE student ADD COLUMN idcard VARCHAR(64) NULL

-- 修改列
ALTER TABLE student MODIFY idcard VARCHAR(128)  NULL

-- 删除列
ALTER TABLE student DROP idcard
```

### 添加约束

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

!> mysql 外建删除的 3 种姿态，1.删除父表，子表记录删除，2.子表关联字段变 null，3.先清空子表关联数据，才能删除父表。

### sql

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



-- 表查询出现的城市

SELECT DISTINCT city
FROM student

-- + 代表相加 字符转化为 0
SELECT 1+1 -- 2
SELECT 'a'+'b' -- 0
SELECT CONCAT('a','b') -- ab


_:单个字符
%:1个或多个

SELECT  *
FROM student
WHERE name LIKE '李%'
-- WHERE name LIKE '%李%' 李—

-- 合并
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

-- 统计课程的最高分 并排序
SELECT course_id ,MAX(grade)
FROM score
GROUP BY course_id
ORDER BY MAX(grade) ASC

-- 统计省份学生大于1的身份
SELECT province ,COUNT(*)
FROM student
GROUP BY province
HAVING COUNT(*)>1

-- 子查询
-- 查询年龄大于平均年龄
SELECT *
FROM student
WHERE age>(SELECT AVG(age)FROM student)

-- 其中一个
SELECT *
FROM student
WHERE age> ANY (SELECT age FROM student WHERE province='北京')

-- 所有
SELECT *
FROM student
WHERE age> ALL (SELECT age FROM student WHERE province='北京')


-- 不在范围内
SELECT *
FROM student
WHERE id NOT IN (SELECT student_id FROM score)


SELECT *
FROM student
WHERE NOT EXISTS  (SELECT * FROM score WHERE score.student_id = student.id )


-- 表链接 多表联查
-- 内链接

-- 左外链接
SELECT * FROM student LEFT JOIN score ON student.id=score.stu_id
-- 右外链接
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

-- 查询父子关联数量
select c1.id ,COUNT(*) FROM cate c1 INNER JOIN cate c2 on c1.id=c2.parent_id
WHERE c1.parent_id=0
GROUP BY c1.id

-- 查询父子关联信息
select c1.id ,c1.name,c2.name AS parentName FROM cate c1 INNER JOIN cate c2 on c1.parent_id=c2.id


-- 查询重复数据  过滤掉
SELECT * FROM cate c1 LEFT JOIN
(SELECT id,name FROM cate GROUP BY name HAVING COUNT(*)>1)c2
ON c1.name =c2.name
WHERE c1.id != c2.id

SELECT * FROM cate c1 WHERE c1.name IN
(SELECT name FROM cate GROUP BY name HAVING COUNT(*)>1)
AND c1.id NOT IN
(SELECT MIX(id) FROM cate GROUP BY name HAVING COUNT(*)>1)

-- 删除重复数据
DELETE  FROM cate
WHERE  name IN
((SELECT name FROM cate GROUP BY name HAVING COUNT(*)>1) t1)
AND c1.id NOT IN
((SELECT MIX(id) FROM cate GROUP BY name HAVING COUNT(*)>1) t2)

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

1.  完整性 不可分割
2.  一致性
3.  事务之间相互隔离
4.  持久性

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

#### 脏读

脏读 就是一个事务读到另一个事务没有提交的数据。事务 A 修改了一个数据，但未提交，事务 B 读到了事务 A 未提交的更新结果，事务 B 读到的就是脏数据。

隔离级别 有四种，分别是：读未提交、读已提交、可重复读、序列化。

1. 读未提交： Read Uncommitted，顾名思义，就是一个事务可以读取另一个未提交事务的数据。最低级别，它存在 4 个常见问题（脏读、不可重复读、幻读、丢失更新）。
2. 读已提交： Read Committed，顾名思义，就是一个事务要等另一个事务提交后才能读取数据。 它解决了脏读问题，存在 3 个常见问题（不可重复读、幻读、丢失更新）。
3. 可重复读： Repeatable Read，就是在开始读取数据（事务开启）时，不再允许修改操作 。它解决了脏读和不可重复读，还存在 2 个常见问题（幻读、丢失更新）。
4. 序列化： Serializable，序列化，或串行化。就是将每个事务按一定的顺序去执行，它将隔离问题全部解决，但是这种事务隔离级别效率低下，比较耗数据库性能，一般不使用。

#### 幻读

幻读：指的是一个事务在前后两次查询同一个范围的时候，后一次查询看到了前一次查询没有看到 的数据行,
一个事务按相同的查询条件重新读取以前检索过的数据，却发现其他事务插入了满足其查询条件的新数据，这种现象就称为"幻读"。
