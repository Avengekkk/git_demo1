# MySQL基本语法

```c++
int main(){
return 0;
}
```

| 姓名   | 班级   | 性别 |
| ------ | ------ | ---- |
| 汪昊   | 计算机 | 男   |
| 管维佳 | 计算机 | 女   |
| 黄其胤 | 土木   | 男   |

以上只是测试一下;

---



## 1.打开命令提示符操作

1. 以管理员身份运行cmd程序

2. 开启程序:net start mysql

3. 登录:用户名:root 密码:87632190wh

4. 格式:mysql -uroot -p87632190wh

5. 进入成功后前面变为mysql

   

## 2.相关操作

### 数据定义语言(DDL)

定义数据库

```mysql
show databases;
-- 展示数据库

create database name;
-- 创建名字为name的数据库(电脑表现出来的文件夹)

drop database name;
-- 删除名字为name的数据库
-- drop database name if exists name;
-- 上面代码的意思是如果name存在就删除

use name;
-- 使用名字为name的数据库

select database();
-- 查看当前使用的数据库

```



定义表

```mysql
show tables;
-- 查询当前数据库下的表

desc tableName;
-- 描述表的结构,desc是description的意思

create table tableName(
	 	variableName1 typeName1,
     	variableName2 typeName2,
     	variableName3 typeName3,
     	variableName4 typeName4,
    .....
);
-- 创建表的结构 

drop table tableName;
-- 删除表

drop table if exists tableName;
-- 如果表存在就删除表

alter table tableName rename to newName;
-- 修改表的名字

alter table tname add columnName type;
-- 新加入一列

alter table tname modify columnName newType;
-- 修改一列的数据类型

alter table tname change columnName newColumnName newType;
-- 修改一列的列名和数据类型

alter table tname drop columnName;
-- 删除名字为column的列

```



|      分类      | 数据类型                    | 数据类型                                       | 数据类型                      |
| :------------: | --------------------------- | ---------------------------------------------- | ----------------------------- |
|    数值类型    | int                         | float                                          | double(总长度,小数点保留位数) |
| 日期和时间类型 | data                        | time                                           | datatime                      |
|   字符串类型   | char(n) 固定长度为n的字符串 | varchar(n) 长度最大为n的字符串,小于n以实际为准 |                               |





### 数据操作语言(DML)

```mysql
select* from tableName;
-- 查询表中的所有数据

insert into tableName(columnName1,columnName2) values(value1,value2);
-- 往表的column1和column2添加数据value1和value2

insert into tableName values(value1,value2,...);
-- 往表所有列添加数据value1和value2....

insert into tableName values(value1,value2....),(value11,value22...);
-- 往表的所有列添加数据value1和value2...之后再添加一行value11,value22...

update tableName set columnName1=value1,columnName2=value2,...[where conditions];
-- 修改表的数据,如果不加where条件的话全部修改

delete from tableName[where conditions];
-- 删除表中的数据,如果不加where条件的话全部删除

```





### 数据查询语言(DQL)

```mysql
-- 基础查询
select columnName from tableName;
-- 从表中查询列名为columnName的数据

select * from tableName;
-- 从表中查询所有的数据

select distinct columnName from tableName;
-- 从表中查询列名为columnName的不重复的数据

select columnName as newName from tableName;
-- 从表中查询列名为columnName(as展示时用newName)的数据


-- 条件查询
select columnName from tableName where conditions;
-- e.g select name from stu where name like "张_";
-- 表示查询所有姓张的同学而不是name="张_";


-- 排序查询
select columnName from tableName order by columnName1 asc(default),columnName2 desc;
-- 默认按照升序排列,先按照column1排列相同就按照column2排列


-- 分组查询
select columnName1,func(columnName2) from tableName group by columnName1 [having conditions];
-- 注意:分组后查询的列为聚合函数和分组的列,查询其他的列没有意
-- where和having的区别
-- 执行时机不一样:where是分组之前进行限定的,不满足where条件不参与分组,而having是分组后对结果进行过滤
-- 可判断的条件不一样:where不能对聚合函数进行判断,having可以

-- 分页查询
select columnName from tableName limit startIndex,searchCount;
-- 起始索引从0开始,起始索引的计算公式=(当前页码-1)*每页显示的条数



-- 聚合函数
select func(columnName) from tableName;




```

| 符号             | 功能                                           |
| ---------------- | ---------------------------------------------- |
| between...and... | 判断是否在两者之间                             |
| in(a,b,c)        | 判断是否是a,b,c当中的其中一个,功能类似于多个或 |
| like "..."       | 模糊查询,_表示单个字符,%表示任意个字符         |
| is null          | 判断是否为null不能用==                         |
| is not null      | 判断是否为null不能用!=                         |

| 函数名            | 功能                       |
| ----------------- | -------------------------- |
| count(columnName) | 统计column有多少行         |
| max(columnName)   | 统计column中最大的那一行   |
| min(columnName)   | 统计column中最小的那一行   |
| sum(columnName)   | 统计column中所有行的和     |
| avg(columnName)   | 统计column中所有行的平均数 |



### 数据控制语言(DCL)

```mysql




```

### 数据约束

| 约束名称 | 描述                                                  | 关键字         |
| -------- | ----------------------------------------------------- | -------------- |
| 非空约束 |                                                       | not null       |
| 唯一约束 |                                                       | unique         |
| 主键约束 | 主键是一行数据的唯一标识,要求非空且唯一               | primary key    |
| 检查约束 | 保证列中的值满足某一条件(MySQL不支持这一个关键字)     | check          |
| 默认约束 |                                                       | default        |
| 外键约束 | 外键用来让两个表之间建立链接,保证数据的一致性和完整性 | foreign key    |
| 自动增长 |                                                       | auto_increment |

#### 外键约束

```mysql
-- 添加约束

-- 创建表时添加外键约束
create table tableName(
    ...
    ...
    [constraint] [key_name] foreign key (外键列名) references 主表(主表列名);
   
);

-- 建完表后添加外键约束
alter table tableName add constraint 外键名称 foreign key (外键字段名称) references 主表名称(主表列名称);

-- 删除约束
alter table tableName drop foreign key 外键名称;

-- key_name->外键名称  的意思是一个表和另一个表建立链接的名称,因为一个表可能和多个表建立链接,所以每个链接要取一个名字来表示区分
-- 外键字段名称是从表的一个列名

```





***



# HTML基本语法

## 1.基础标签

| 标签      |               描述               |
| --------- | :------------------------------: |
| <front>   | 定义文本的字体,字体尺寸,字体颜色 |
| <b>       |           定义粗体文本           |
| <i>       |           定义斜体文本           |
| <u>       |          定义文本下划线          |
| <center>  |           定义文本居中           |
| <p>       |             定义段落             |
| <br>      |             定义拆行             |
| <hr>      |            定义水平线            |
| <h1>-<h6> |      定义标题,h1最大,h6最小      |
| <a>       |            定义超链接            |



### 相关案例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>基础Test</title>
</head>
<body>

<h1>
    <font color="green" face="隶书" size="10">
        这是第一级标题
    </font>
</h1>
<h2>
    <font color="pink">
        这是第二级标题
    </font>
</h2>
<h3>
    这是第三级标题
</h3>

<hr><font color="blue">


<!-- 上面这是水平分割线-->
我是分割线
<hr>
</font>

汪昊<br>
牛逼

<p>

    <b>
        别问,
    </b>
</p>
<p>

<center>
    问就是我是段落
</center>
</p>


</body>




<head>
    图片Test
</head>
<body>
<h1>
    这里测试图片
</h1>
<!--<img src="https://p3.ssl.qhimgs1.com/sdr/400__/t015d35297bb167853d.jpg">-->
<img src="./img/clash.png" width="1000" height="500" >
<img src="./img/公孙离.jpg">



</body>

</html>
```



## 2.列表标签

| 标签 |     描述     |
| ---- | :----------: |
| <ol> | 定义有序列表 |
| <ul> | 定义无序列表 |
| <li> |  定义列表项  |

### 相关案例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>超链接标签</title>
</head>
<body>


<a href="https://www.jetbrains.com/" target="_blank">
  这是jetbrain的官网
</a>

<p>
    排名
</p>

<ol type="A">
    <li>
        汪昊
    </li>
    <li>
        张三
    </li>
    <li>
        李四
    </li>

</ol>
<!--有序列表-->

成员名单
<ul>
    <li>
        汪昊
    </li>
    <li>
        张三
    </li>
    <li>
        李四
    </li>

</ul>



</body>
</html>
```





## 3.表格标签

| 标签    |      描述      |
| ------- | :------------: |
| <table> |    定义表格    |
| <tr>    |     定义行     |
| <td>    |   定义单元格   |
| <th>    | 定义表头单元格 |

### 相关案例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>测试表格标签</title>
</head>
<body>

<table border="2" cellspacing="0" width="500" >
    <tr>
<!--  定义表头-->
    <th>
        ID
    </th>
    <th>
        图片
    </th>
    <th>
        名称
    </th>
    </tr>

    <tr align="center">
<!-- <td rowspan="2"> 合并2行-->
        <td>
            001
        </td>
        <td>
            <img src="./img/clash.png" width="50" height="50">
        </td>
        <td>
            皇室战争
        </td>

    </tr>
    <tr align="center">
<!--  <td colspan="2"> 合并2列 -->
        <td>
            002
        </td>
        <td>
            <img src="./img/公孙离.jpg" width="50" height="50">
        </td>
        <td>
            公孙离
        </td>
    </tr>






</table>

<p>

</p>


<div>
    我占领了一整行
</div>
<div>
    我也是
</div>

<span>
    我很节约,没有占领一整行
</span>
<span>
    所以我们在一行了
</span>

</body>
</html>
```



## 4.表单标签

| 标签       |                描述                 |
| ---------- | :---------------------------------: |
| <form>     |              定义表单               |
| <input>    | 定义表单项,通过type属性控制输入形式 |
| <label>    |           为表单定义标注            |
| <select>   |            定义下拉列表             |
| <option>   |        定义下拉列表的列表项         |
| <textarea> |             定义文本域              |

#### 注意:

form标签的两个属性:method和action

action:指定表单数据提交的URL

​			表单数据要被提交必须指定name属性(此处name特指input的name属性)

method:指定表单提交的方式(form属性值)

​			1.get:默认值(请求参数会拼接在URL后面,URL的长度限制为4KB)

​			2.post:请求参数会在http请求协议的请求体中(请求参数无限制)

#### input中type的相关操作

| type取值 |                     描述                      |
| -------- | :-------------------------------------------: |
| text     |           默认值,定义单行的输入字段           |
| password |                 定义密码字段                  |
| radio    |                 定义单选按钮                  |
| checkbox |                  定义复选框                   |
| file     |               定义文件上传按钮                |
| hidden   |              定义隐藏的输入字段               |
| submit   | 定义提交按钮,提交按钮会把表单数据发送到服务器 |
| reset    |  定义重置按钮,重置按钮会清除表单中的所有数据  |
| button   |                定义可点击按钮                 |

### 相关案例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>表单标签</title>
</head>
<body>


<!--<form action="#" method="post">-->
<!--    <input type="text" name="accept">-->
<!--    <input type="submit">-->
<!--</form>-->


<form action="#" method="post">
    <label for="userName">
        用户名:
    </label>
    <input type="text" name="userName" id="userName">
    <br>

    <label for="password">
        密 码:
    </label>
    <input type="password" name="password" id="password">
    <br>
    <label for="male">
        性别:
    </label>
    <input type="radio" name="gender" value="1" id="male"> 男
    <input type="radio" name="gender" value="0" id="female"> 女
    <br>

    爱好:
    <input type="checkbox" name="hobby" value="hobby1" id="hobby1">
    <label for="hobby1">
        打游戏
    </label>
    <input type="checkbox" name="hobby" value="hobby1" id="hobby2">
    <label for="hobby2">
        游泳
    </label>
    <input type="checkbox" name="hobby" value="hobby1" id="hobby3">
    <label for="hobby3">
        跑步
    </label>
    <br>

    图像
    <input type="file" name="photo">
    <br>
    城市
    <select name="city">
        <option value="beijing">
            北京
        </option>
        <option>
            天津
        </option>
        <option>
            武汉
        </option>
        <option>
            南京
        </option>

    </select>
    <br>

    <label for="intro">
        自我介绍
    </label>
    <textarea name="introduceMyself" id="intro" cols="5" rows="3">

    </textarea>


    <br>
    <input type="submit" value="提交">
    <input type="reset" value="取消">
    <input type="button" value="返回">

</form>


</body>
</html>
```

# CSS基本语法

## CSS导入方式

### 1.内部样式

定义<style>标签,在标签内部定义CSS样式

#### 相关案例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>CSS导入方法</title>
    <style>
        span{
        color:red;
        }
    
    </style>

    <style>
        special{
        color:pink;
        }

    </style>

</head>
<body>

<!--<div style="color:blue">-->
<!--    hello world-->
<!--</div>-->


<span>
    汪昊
</span>

<special>
    你好

</special>


</body>
</html>
```



### 2.外部样式

定义link标签引入外部CSS文件

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>CSS导入方法</title>
    
    <!--  导入CSS文件  -->
    <link href="../CSS/demo1.css" rel="stylesheet">
    <!-- rel是指定要解析文件的类型 -->

</head>
<body>

<fileImport>
    这是第二种方法,利用CSS文件导入方式
</fileImport>


</body>
</html>
```

```css
<!-- CSS文件 -->
fileImport{
color:green;
}
```

## CSS选择器

概念:选择器是用特定的方式选择你要用于CSS的对象

| 名称       |                    样式                     | 说明                                                         | 示例                                                         |
| ---------- | :-----------------------------------------: | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 元素选择器 | 元素名称{color:red;}(color:red只是一个例子) | 与上面内部样式一样,用于选择大量的带有同一标签的语句          | div{color:red;}                                              |
| ID选择器   |            #ID属性值{color:red;}            | 因为ID标识是唯一的,所以ID选择器用来选择唯一的一条语句        | #name{color:red;}               <div id="name"> hello world</div> |
| 类选择器   |          .class属性值{color.red;}           | 用于选择一类语句,即凡是和class属性相同的语句皆能被选中,与ID不同的是,ID只能选择唯一一个,而class可以选择多个,即使标签不同 | .cls{color:red;}                      <div class="cls"> hello world</div> |

注意:上面的.cls和#name语句都要放在style当中
