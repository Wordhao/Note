mysql复习



* 创建CREATE

```mysql
CREATE TABLE `table_name`(
    `id` INT(10) NOT NULL,
    `mobile` VARCHAR(11) NOT NULL,
    `nickname` datetime,
    PRIMARY KEY(`id`)
)ENGINE=InnoDB DEFAULT  CHARSET=utf8;
//InnoDB储存引擎，utf8编码方式
```



* 插入INSERT

```mysql
INSERT INTO `table_name`(`id`,`mobile`)
       VALUES(1,'123456'),
             (2,'123445');
```



* 查询SELECT

```mysql
SELECT id,name FROM timi_adc;
```

​                  字段名                 表名



条件查询WHERE

待补充（查询优化）

模糊查询**LIKE/NOT LIKE**

```mysql
WHERE hero_name LIKE '%孙%';//含孙
WHERE hero_name LIKE '孙%';//孙开头
WHERE hero_name LIKE '%孙';//孙结尾
WHERE hero_name LIKE '_孙香';//x尚香
WHERE hero_name NOT LIKE '%孙%';//不含孙
```

条件复合**AND&OR**

```mysql

```

条件归属**IN/NOT IN**

```mysql
SELECT * FROM timi_adc WHERE fever IN('T0','T3');
```



Limit子句

```mysql
SELECT * FROM timi_adc WHERE xxx LIMIT x,y;
```

从第x+1行开始查，到第y行。

（LIMIT x   等价于  LIMIT 0，x；）



排序ORDER BY

```mysql
SELECT * from table_name ORDER BY field_name;//升序
```

ORDER BY field_name *DESC*;//降序



* 更新UPDATE

```mysql
UPDATE timi_adc SET ban_rate=0.01 WHERE hero_name = '艾琳';
```

* 删除DELETE

```mysql
DELETE FROM user WHERE id=4;
```





字符串处理

* **CONCAT**拼接

```mysql
SELECT id,concat(hero_name,'的胜率是',win_rate) FROM timi_adc;
```

* **TRIM**去空格

```mysql
SELECT trim(hero_name),trim(fever) FROM timi_adc WHERE id = 20;
```



```mysql
TRIM( BOTH|LEADING|TRAILING removed_str FROM str);
```

​              前后空格|前空格|后空格

```mysql
SELECT
  TRIM(
    TRAILING 'Q'
    FROM
      fever
  )
FROM
  timi_adc
WHERE
  id = 21;
```



***关联查询***

* 左连接 **LEFT JOIN**

```mysql
SELECT
  *
FROM
  TableA LEFT  JOIN
  TableB
  ON condition;
```

```mysql
SELECT
  *
FROM
  ykd_teacher
  LEFT JOIN ykd_course ON ykd_teacher.id = ykd_course.teacher_id;
```



* 右连接 **RIGHT JOIN**

(左连接返回左表内数据，右连接返回右表内数据)



* 内连接**INNER JOIN**

 ![img](https://style.youkeda.com/newcoursep4/d1/d1-5/A%26B.jpg?x-oss-process=image/resize,w_800/watermark,image_d2F0ZXJtYXNrLnBuZz94LW9zcy1wcm9jZXNzPWltYWdlL3Jlc2l6ZSx3XzEwMA==,t_60,g_se,x_10,y_10) 

```mysql
SELECT
  *
FROM
  Table_A
  INNER JOIN Table_B
ON
  Table_A.id = Table_B.student_id;
```



* **UNION**查询所有内容

```mysql
SELECT
  *
FROM
  Table_A
  LEFT JOIN Table_B
ON
  Table_A.id = Table_B.student_id
UNION DISTINCT
SELECT
  *
FROM
  Table_A
  RIGHT JOIN Table_B ON Table_A.id=Table_B.student_id;
```



