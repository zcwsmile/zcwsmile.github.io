---
layout: post
title: MYSQL的常用命令和增删改查
category: 技术
tags: [Pattern]
keywords: MSSQL
---
   
连接命令：mysql -h[主机地址] -u[用户名] -p[用户密码]  
创建数据库：create database [库名]  
显示所有数据库: show databases;  
打开数据库:use [库名]  
当前选择的库状态:SELECT DATABASE();  
创建数据表:CREATE TABLE [表名]([字段名] [字段类型]([字段要求]) [字段参数], ......);  
显示数据表字段:describe 表名;  
当前库数据表结构:show tables;  
更改表格　  
  ALTER TABLE [表名] ADD COLUMN [字段名] DATATYPE  
  说明：增加一个栏位（没有删除某个栏位的语法。  
  ALTER TABLE [表名] ADD PRIMARY KEY ([字段名])  
  说明：更改表得的定义把某个栏位设为主键。  
  ALTER TABLE [表名] DROP PRIMARY KEY ([字段名])  
  说明：把主键的定义删除。
  修改表中字段的名：  MSSQL:   EXECUTE sp_rename  N'dbo.e_table.date',  N'datetest',  'COLUMN';
   (sqlite 不支持)       MySQL:   ALTER TABLE 表名 CHANGE 旧字段名 新字段名 新数据类型
显示当前表字段:show columns from tablename;  
删库:drop database [库名];  
删表:drop table [表名]；  
数据操作  
添加：INSERT INTO [表名] VALUES('','',......顺序排列的数据);  
查询: SELECT * FROM [表名] WHERE ([条件]);  
建立索引:CREATE INDEX [索引文件名] ON [表名] ([字段名]);  
删除：DELETE FROM [表名] WHERE ([条件]);  
修改：UPDATE [表名] SET [修改内容如name = 'Mary'] WHERE [条件]；  
  
导入外部数据文本:  
1.执行外部的sql脚本  
当前数据库上执行:mysql < input.sql  
指定数据库上执行:mysql [表名] < input.sql  
2.数据传入命令 load data local infile "[文件名]" into table [表名];  
备份数据库：(dos下)  
mysqldump --opt school>school.bbb  

提示：常用MySQL命令以";"结束,有少量特殊命令不能加";"结束，如备份数据库  
一. 增删改查操作  
  
=================================================================================  
1. 增:  
insert into 表名 values(0,'测试');  
注：如上语句，表结构中有自动增长的列，也必须为其指定一个值，通常为0  
insert into 表名(id,name) values(0,'尹当')--同上  
2.删数据:  
delete from 表名;  
delete from 表名 where id=1;  
删除结构：  
删数据库：drop database 数据库名;  
删除表：drop table 表名;  
删除表中的列:alter table 表名 drop column 列名;  
3. 改:  
修改所有：update 表名 set 列名='新的值，非数字加单引号' ;  
带条件的修改：update 表名 set 列名='新的值，非数字加单引号' where id=6;  
4.查:  
查询所有的数据：select *from 表名;  
带条件的查询：  
select *from 表名 where 列名=条件值;  
Select * from 表名 where 列名 not like（like） '字符值'  
分页查询：select *from 表名 limit 每页数量 offset 偏移量;  
  
二.操作命令  
=================================================================================  
1. 查看数据库信息：show databases;  
2.查看表信息：show tables;  
3.查看表的结构：desc 表名  
4. 新建数据库:create database 数据库名;  
5.操作指定数据库:use 数据库名;  
6.新建数据表(先use 操作库);  
create table 表名(规范为tbl_表名)  
(  
id int auto_increment primary key,( auto_increment为自动增长)  
name varchar(20) primary key  
)ENGINE=InnoDB DEFAULT CHARSET=gbk//支持事务和设置表的编码  
6.2添加主外键：  
alter table 外表名  add constraint FK_名称 foreign key(外列) references 主表名(主列)  
如现有两表 主表tbl_order 子表tbl_orderdetail 现子表tbl_orderdetail的oid列引用了主表tbl_order的oid列  
则命令如下：  
alter table tbl_orderdetail  add constraint FK_oid foreign key(oid) references tbl_order(oid)  
7.导出表，备份到一个文件中，如.txt,.doc  
cmd命令窗口：mysqldump -u 用户名  -p  需要备份的数据库名 >备份的文件的保存路径和文件名  
注：如指定的文件不存在，mysql会自动添加一个文件，此命令不能加分号结尾（文件没有备份建数据库操作）  
8.导入数据库备份文件：  
(1).在mysql命令窗口  
(2).新建一个要导入的数据库(因为备份中没有备份建数据库操作)  
(3).use 当前库名  
(4).source 备份的文件的保存路径和文件名(此命令不能加分号结尾)  
  
三：系统操作  
=================================================================================  
1. 打开服务:net start mysql(mysql为配置时，可自定名称)  
2.关闭服务:net stop mysql  
3.从cmd 模式进入mysql  
(1).mysql -u 用户名 -p 回车>输入正确密码>进入欢迎  
(2).mysql -h IP(本机localhost) -u 用户名 -p 回车>输入正确密码>进入欢迎  
3.退出：exit/quit;  
4.修改用户密码:mysqladmin -u 用户名 -p password 新密码  
5.处理中文乱码：  
(1).在D:/MySQL /MySQL Server 5.0/data的操作数据为文件中查看是否为以下：  
default-character-set=gbk  
default-collation=gbk_chinese_ci  
  
(2).查看安装文件默认编码：D:/MySQL/MySQL Server 5.0>my>default-character-set=gbk  
  
=================================================================================  
启动：net start mySql;  
进入：mysql -u root -p/mysql -h localhost -u root -p databaseName;  
列出数据库：show databases;  
选择数据库：use databaseName;  
列出表格：show tables；  
显示表格列的属性：show columns from tableName；  
建立数据库：source fileName.txt;  
匹配字符：可以用通配符_代表任何一个字符，％代表任何字符串;  
增加一个字段：alter table tabelName add column fieldName dateType;  
增加多个字段：alter table tabelName add column fieldName1 dateType,add columns fieldName2 dateType;  
多行命令输入:注意不能将单词断开;当插入或更改数据时，不能将字段的字符串展开到多行里，否则硬回车将被储存到数据中;  
增加一个管理员帐户：grant all on *.* to user@localhost identified by "password";  
每条语句输入完毕后要在末尾填加分号';'，或者填加'/g'也可以；  
查询时间：select now();  
查询当前用户：select user();  
查询数据库版本：select version();  
查询当前使用的数据库：select database();  
  
1、删除student_course数据库中的students数据表：  
rm -f student_course/students.*  
  
2、备份数据库：(将数据库test备份)  
mysqldump -u root -p test>c:/test.txt  
备份表格：(备份test数据库下的mytable表格)  
mysqldump -u root -p test mytable>c:/test.txt  
将备份数据导入到数据库：(导回test数据库)  
mysql -u root -p test  
  
3、创建临时表：(建立临时表zengchao)  
create temporary table zengchao(name varchar(10));  
  
4、创建表是先判断表是否存在  
create table if not exists students(……);  
  
5、从已经有的表中复制表的结构  
create table table2 select * from table1 where 1<>1;  
  
6、复制表  
create table table2 select * from table1;  
  
7、对表重新命名  
alter table table1 rename as table2;  
  
8、修改列的类型  
alter table table1 modify id int unsigned;//修改列id的类型为int unsigned  
alter table table1 change id sid int unsigned;//修改列id的名字为sid，而且把属性修改为int unsigned  
  
9、创建索引  
alter table table1 add index ind_id (id);  
create index ind_id on table1 (id);  
create unique index ind_id on table1 (id);//建立唯一性索引  
  
10、删除索引  
drop index idx_id on table1;  
alter table table1 drop index ind_id;  
  
11、联合字符或者多个列(将列id与":"和列name和"="连接)  
select concat(id,':',name,'=') from students;  
  
12、limit(选出10到20条)<第一个记录集的编号是0>  
select * from students order by id limit 9,10;  
  
13、MySQL不支持的功能  
事务，视图，外键和引用完整性，存储过程和触发器  
  
  
14、MySQL会使用索引的操作符号  
<,<=,>=,>,=,between,in,不带%或者_开头的like  
  
15、使用索引的缺点  
1)减慢增删改数据的速度；  
2）占用磁盘空间；  
3）增加查询优化器的负担；  
当查询优化器生成执行计划时，会考虑索引，太多的索引会给查询优化器增加工作量，导致无法选择最优的查询方案；  
  
16、分析索引效率  
方法：在一般的SQL语句前加上explain；  
分析结果的含义：  
1）table：表名；  
2）type：连接的类型，(ALL/Range/Ref)。其中ref是最理想的；  
3）possible_keys：查询可以利用的索引名；  
4）key：实际使用的索引；  
5）key_len：索引中被使用部分的长度（字节）；  
6）ref：显示列名字或者"const"（不明白什么意思）；  
7）rows：显示MySQL认为在找到正确结果之前必须扫描的行数；  
8）extra：MySQL的建议；  
  
17、使用较短的定长列  
1）尽可能使用较短的数据类型；  
2）尽可能使用定长数据类型；  
a）用char代替varchar，固定长度的数据处理比变长的快些；  
b）对于频繁修改的表，磁盘容易形成碎片，从而影响数据库的整体性能；  
c）万一出现数据表崩溃，使用固定长度数据行的表更容易重新构造。使用固定长度的数据行，每个记录的开始位置都是固定记录长度的倍数，可以很容易被检测到，但是使用可变长度的数据行就不一定了；  
d）对于MyISAM类型的数据表，虽然转换成固定长度的数据列可以提高性能，但是占据的空间也大；  
  
18、使用not null和enum  
尽量将列定义为not null，这样可使数据的出来更快，所需的空间更少，而且在查询时，MySQL不需要检查是否存在特例，即null值，从而优化查询；  
如果一列只含有有限数目的特定值，如性别，是否有效或者入学年份等，在这种情况下应该考虑将其转换为enum列的值，MySQL处理的更快，因为所有的enum值在系统内都是以标识数值来表示的；  
  
19、使用optimize table  
对于经常修改的表，容易产生碎片，使在查询数据库时必须读取更多的磁盘块，降低查询性能。具有可变长的表都存在磁盘碎片问题，这个问题对blob数据类型更为突出，因为其尺寸变化非常大。可以通过使用optimize table来整理碎片，保证数据库性能不下降，优化那些受碎片影响的数据表。 optimize table可以用于MyISAM和BDB类型的数据表。实际上任何碎片整理方法都是用mysqldump来转存数据表，然后使用转存后的文件并重新建数据表；  
  
20、使用procedure analyse()  
可以使用procedure analyse()显示最佳类型的建议，使用很简单，在select语句后面加上procedure analyse()就可以了；例如：  
select * from students procedure analyse();  
select * from students procedure analyse(16,256);  
第二条语句要求procedure analyse()不要建议含有多于16个值，或者含有多于256字节的enum类型，如果没有限制，输出可能会很长；  
  
21、使用查询缓存  
1）查询缓存的工作方式：  
第一次执行某条select语句时，服务器记住该查询的文本内容和查询结果，存储在缓存中，下次碰到这个语句时，直接从缓存中返回结果；当更新数据表后，该数据表的任何缓存查询都变成无效的，并且会被丢弃。  
2）配置缓存参数：  
变量：query_cache _type，查询缓存的操作模式。有3中模式，0：不缓存；1：缓存查询，除非与 select sql_no_cache开头；2：根据需要只缓存那些以select sql_cache开头的查询； query_cache_size：设置查询缓存的最大结果集的大小，比这个值大的不会被缓存。  
  
22、调整硬件  
1）在机器上装更多的内存；  
2）增加更快的硬盘以减少I/O等待时间；  
寻道时间是决定性能的主要因素，逐字地移动磁头是最慢的，一旦磁头定位，从磁道读则很快；  
3）在不同的物理硬盘设备上重新分配磁盘活动；  
如果可能，应将最繁忙的数据库存放在不同的物理设备上，这跟使用同一物理设备的不同分区是不同的，因为它们将争用相同的物理资源（磁头）。  
  

一、连接MYSQL。  
  
格式： mysql -h主机地址 -u用户名 －p用户密码  
  
1、例1：连接到本机上的MYSQL。  
  
首先在打开DOS窗口，然后进入目录 mysqlbin，再键入命令mysql -uroot -p，回车后提示你输密码，如果刚安装好MYSQL，超级用户root是没有密码的，故直接回车即可进入到MYSQL中了，MYSQL的提示符是：mysql>  
  
2、例2：连接到远程主机上的MYSQL。假设远程主机的IP为：110.110.110.110，用户名为 root,密码为abcd123。则键入以下命令：  
  
mysql -h110.110.110.110 -uroot -pabcd123  
  
（注:u与root可以不用加空格，其它也一样）  
  
3、退出MYSQL命令： exit （回车）  
  
二、修改密码。  
  
格式：mysqladmin -u用户名 -p旧密码 password 新密码  
  
1、例1：给root加个密码ab12。首先在DOS下进入目录mysqlbin，然后键入以下命令  
  
mysqladmin -uroot -password ab12  
  
注：因为开始时root没有密码，所以-p旧密码一项就可以省略了。  
  
2、例2：再将root的密码改为djg345。  
  
mysqladmin -uroot -pab12 password djg345  
  
三、增加新用户。（注意：和上面不同，下面的因为是MYSQL环境中的命令，所以后面都带一个分号作为命令结束符）  
  
格式：grant select on 数据库.* to 用户名@登录主机 identified by /"密码/"  
  
例1、增加一个用户test1密码为abc，让他可以在任何主机上登录，并对所有数据库有查询、插入、修改、删除的权限。首先用以root用户连入MYSQL，然后键入以下命令：  
  
grant select,insert,update,delete on *.* to test1@/"%/" Identified by /"abc/";  
  
但例1增加的用户是十分危险的，你想如某个人知道test1的密码，那么他就可以在internet上的任何一台电脑上登录你的mysql数据库并对你的数据可以为所欲为了，解决办法见例2。  
  
例 2、增加一个用户test2密码为abc,让他只可以在localhost上登录，并可以对数据库mydb进行查询、插入、修改、删除的操作（localhost指本地主机，即MYSQL数据库所在的那台主机），这样用户即使用知道test2的密码，他也无法从 internet上直接访问数据库，只能通过MYSQL主机上的web页来访问了。  
  
grant select,insert,update,delete on mydb.* to test2@localhost identified by /"abc/";  
  
如果你不想test2有密码，可以再打一个命令将密码消掉。  
  
grant select,insert,update,delete on mydb.* to test2@localhost identified by /"/";  
  
在上篇我们讲了登录、增加用户、密码更改等问题。下篇我们来看看MYSQL中有关数据库方面的操作。注意：你必须首先登录到MYSQL中，以下操作都是在MYSQL的提示符下进行的，而且每个命令以分号结束。  
  
一、操作技巧  
  
1、如果你打命令时，回车后发现忘记加分号，你无须重打一遍命令，只要打个分号回车就可以了。也就是说你可以把一个完整的命令分成几行来打，完后用分号作结束标志就OK。  
  
2、你可以使用光标上下键调出以前的命令。但以前我用过的一个MYSQL旧版本不支持。我现在用的是mysql- 3.23.27-beta-win。  
  
二、显示命令  
  
1、显示数据库列表。  
  
show databases;  
  
刚开始时才两个数据库：mysql和test。mysql库很重要它里面有MYSQL的系统信息，我们改密码和新增用户，实际上就是用这个库进行操作。  
  
2、显示库中的数据表：  
  
use mysql； ／／打开库，学过FOXBASE的一定不会陌生吧  
  
show tables;  
  
3、显示数据表的结构：  
  
describe 表名;  
  
4、建库：  
  
create database 库名;  
  
5、建表：  
  
use 库名；  
  
create table 表名 (字段设定列表)；  
  
6、删库和删表:  
  
drop database 库名;  
  
drop table 表名；  
  
7、将表中记录清空：  
  
delete from 表名;  
  
8、显示表中的记录：  
  
select * from 表名;  
  
三、一个建库和建表以及插入数据的实例  
  
drop database if exists school; //如果存在SCHOOL则删除  
  
create database school; //建立库SCHOOL  
  
use school; //打开库SCHOOL  
  
create table teacher //建立表TEACHER  
  
(  
  
id int(3) auto_increment not null primary key,  
  
name char(10) not null,  
  
address varchar(50) default ’深圳’,  
  
year date  
  
); //建表结束  
  
//以下为插入字段  
  
insert into teacher values(’’,’glchengang’,’深圳一中’,’1976-10-10’);  
  
insert into teacher values(’’,’jack’,’深圳一中’,’1975-12-23’);  
  
注：在建表中（1）将ID设为长度为3的数字字段:int(3)并让它每个记录自动加一:auto_increment并不能为空:not null而且让他成为主字段primary key（2）将NAME设为长度为10的字符字段（3）将ADDRESS设为长度50的字符字段，而且缺省值为深圳。varchar和char有什么区别呢，只有等以后的文章再说了。（4）将YEAR设为日期字段。  
  
如果你在mysql提示符键入上面的命令也可以，但不方便调试。你可以将以上命令原样写入一个文本文件中假设为 school.sql，然后复制到c://下，并在DOS状态进入目录//mysql//bin，然后键入以下命令：  
  
mysql -uroot -p密码 < c://school.sql  
  
如果成功，空出一行无任何显示；如有错误，会有提示。（以上命令已经调试，你只要将//的注释去掉即可使用）。  
  
四、将文本数据转到数据库中  
  
1、文本数据应符合的格式：字段数据之间用tab键隔开，null值用//n来代替.  
  
例：  
  
3 rose 深圳二中 1976-10-10  
  
4 mike 深圳一中 1975-12-23  
  
2、数据传入命令 load data local infile /"文件名/" into table 表名;  
  
注意：你最好将文件复制到//mysql//bin目录下，并且要先用use命令打表所在的库。  
  
五、备份数据库：（命令在DOS的//mysql//bin目录下执行）  
mysqldump --opt school>school.bbb  
  
注释:将数据库school备份到school.bbb文件，school.bbb是一个文本文件，文件名任取，打开看看你会有新发现。  
  
   
  
mysql命令行常用命令  
  
第一招、mysql服务的启动和停止  
net stop mysql  
net start mysql  
第二招、登陆mysql  
语法如下： mysql -u用户名 -p用户密码  
键入命令mysql -uroot -p， 回车后提示你输入密码，输入12345，然后回车即可进入到mysql中了，mysql的提示符是：  
mysql>  
注意，如果是连接到另外的机器上，则需要加入一个参数-h机器IP  
第三招、增加新用户  
格式：grant 权限 on 数据库.* to 用户名@登录主机 identified by "密码"  
如，增加一个用户user1密码为password1，让其可以在本机上登录， 并对所有数据库有查询、插入、修改、删除的权限。首先用以root用户连入mysql，然后键入以下命令：  
grant select,insert,update,delete on *.* to user1@localhost Identified by "password1";  
如果希望该用户能够在任何机器上登陆mysql，则将localhost改为"%"。  
如果你不想user1有密码，可以再打一个命令将密码去掉。  
grant select,insert,update,delete on mydb.* to user1@localhost identified by "";  
第四招： 操作数据库  
登录到mysql中，然后在mysql的提示符下运行下列命令，每个命令以分号结束。  
1、 显示数据库列表。  
show databases;  
缺省有两个数据库：mysql和 test。 mysql库存放着mysql的系统和用户权限信息，我们改密码和新增用户，实际上就是对这个库进行操作。  
2、 显示库中的数据表：  
use mysql;  
show tables;  
3、 显示数据表的结构：  
describe 表名;  
4、 建库与删库：  
create database 库名;  
drop database 库名;  
5、 建表：  
use 库名;  
create table 表名(字段列表);  
drop table 表名;  
6、 清空表中记录：  
delete from 表名;  
7、 显示表中的记录：  
select * from 表名;  
第五招、导出和导入数据  
1. 导出数据：  
mysqldump --opt test > mysql.test  
即将数据库test数据库导出到mysql.test文件，后者是一个文本文件  
如：mysqldump -u root -p123456 --databases dbname > mysql.dbname  
就是把数据库dbname导出到文件mysql.dbname中。  
2. 导入数据:  
mysqlimport -u root -p123456 < mysql.dbname。  
不用解释了吧。  
3. 将文本数据导入数据库:  
文本数据的字段数据之间用tab键隔开。  
use test;  
load data local infile "文件名" into table 表名;  
  
SQL常用命令使用方法：  
  
(1) 数据记录筛选：  
  
sql="select * from 数据表 where 字段名=字段值 order by 字段名 [desc]"  
  
sql="select * from 数据表 where 字段名 like '%字段值%' order by 字段名 [desc]"  
  
sql="select top 10 * from 数据表 where 字段名 order by 字段名 [desc]"  
  
sql="select * from 数据表 where 字段名 in ('值1','值2','值3')"  
  
sql="select * from 数据表 where 字段名 between 值1 and 值2"  
  
(2) 更新数据记录：  
  
sql="update 数据表 set 字段名=字段值 where 条件表达式"  
  
sql="update 数据表 set 字段1=值1,字段2=值2 …… 字段n=值n where 条件表达式"  
  
(3) 删除数据记录：  
  
sql="delete from 数据表 where 条件表达式"  
  
sql="delete from 数据表" (将数据表所有记录删除)  
  
(4) 添加数据记录：  
  
sql="insert into 数据表 (字段1,字段2,字段3 …) values (值1,值2,值3 …)"  
  
sql="insert into 目标数据表 select * from 源数据表" (把源数据表的记录添加到目标数据表)  
  
(5) 数据记录统计函数：  
  
AVG(字段名) 得出一个表格栏平均值  
COUNT(*|字段名) 对数据行数的统计或对某一栏有值的数据行数统计  
MAX(字段名) 取得一个表格栏最大的值  
MIN(字段名) 取得一个表格栏最小的值  
SUM(字段名) 把数据栏的值相加  
  
引用以上函数的方法：  
  
sql="select sum(字段名) as 别名 from 数据表 where 条件表达式"  
set rs=conn.excute(sql)  
  
用 rs("别名") 获取统的计值，其它函数运用同上。  
  
(6) 数据表的建立和删除：  
  
CREATE TABLE 数据表名称(字段1 类型1(长度),字段2 类型2(长度) …… )  
  
例：CREATE TABLE tab01(name varchar(50),datetime default now())  
  
DROP TABLE 数据表名称 (永久性删除一个数据表)  
  
  
  
select * from test.text where 1 *表示所有栏目 test指数据库名text指表名 where指条件  
Select remark as r id,uid from test.text where 指id uid 2栏显示 as 就是给栏目命名   
select * from test.text where id>4 指ID大于4的都显示出来  
select * from test.text where id<>4 指ID 不等于4的都出来  
select * from test.text where id=1 指ID等于1的出来  
select * from test.text where id in(1,3,5) 指找出ID为1 3 5的 not in（）则相反  
select * from test.text where uid like "%王%" 指UID里只要带王字的都出来 %王 表示什么王 ，王%表示 王什么。  
select * from test.text where remark like "%学%" 指remark里带学的都出来  
select * from test.text where id between 1 and 10 and uid like "%王%"表示ID 1-10 并且 UID带王字的出来  
select * from test.text where id not between 1 and 4   指ID不在1-4里面的 出来  
（1 and 2 表示满足1且满足2     1 or 2 表示满足1和满足2 ）and or可以连接很多条件  
select * from test.text group by remark 显示列出remark有多少类别 如图↓ 有5类 group by 就是分组命令  
  
select * from test.text order by regdate asc 把regdate 按从小到大排列   
ASC不打就是默认从小到大 DESC表示从大到小 如 order desc  
select * from test.text order by regdate asc,id desc 这样就查询出日期从小到大 然后在满足日期的排列后 ID从大到小排列  
select * from test.text limit 0,5 表示取5条记录 如果是3，6 那就是第4-第9条记录被取出 如图↓  
如过只写一个6那就等于0，6  
select * from test.text group by remark order by regdate limit 6   先分组 再排序 LIMIT放最后 这是语法不能颠倒。  
select count(id) from test.text count()表示查询有多少条信息 这样根据表显示出10条  
select max(regdate) from test.text max() 查询最大值 只能针对数字 包括日期 根据表显示出2008-10-22 14:41:30  
select min(regdate)from test.text min() 查询最小值 只能针对数字 包括日期 根据表显示出2008-10-07 13:21:32  
select avg(id) from test.text   avg() 查询平均值 也只针对数字 包括日期 显示出5.5 如算平均分数  
select sum(id) from test.text   sum() 查询累计值 数字包括日期 显示出55 1+2+3+。。10=55 如算总分数  
insert 插入语句  
insert into `text`(`id`,`uid`,`regdate`,`remark`)values(null,'ken',now(),'学生') 其中null就是没有 now()就是时间日期自动生成  
字段的类型要设计好。特别注意！  
  
  
  
  
Update 更改语句  
Update 表名 set 字段=值 where 条件 LIMIT（可省略）  
update test.text set uid='kenchen' where id=11   意思是把ID是11的UID 改成kenchen  
  
Delete 删除语句  
Delete from 表命 where limit   
Delete from text where id=3 意思是把ID=3的信息条删除！  
  
mysql 字段类型说明- -  
  
  
MySQL支持大量的列类型，它可以被分为3类：数字类型、日期和时间类型以及字符串(字符)类型。本节首先给出可用类型的一个概述，并且总结每个列类型的存储需求，然后提供每个类中的类型性质的更详细的描述。概述有意简化，更详细的说明应该考虑到有关特定列类型的附加信息，例如你能为其指定值的允许格式。   
  
由MySQL支持的列类型列在下面。下列代码字母用于描述中：   
  
M   
指出最大的显示尺寸。最大的合法的显示尺寸是 255 。   
D   
适用于浮点类型并且指出跟随在十进制小数点后的数码的数量。最大可能的值是30，但是应该不大于M-2。   
方括号(“[”和“]”)指出可选的类型修饰符的部分。   
  
注意，如果你指定一个了为ZEROFILL，MySQL将为该列自动地增加UNSIGNED属性。   
  
TINYINT[(M)] [UNSIGNED] [ZEROFILL]   
一个很小的整数。有符号的范围是-128到127，无符号的范围是0到255。   
  
  
SMALLINT[(M)] [UNSIGNED] [ZEROFILL]   
一个小整数。有符号的范围是-32768到32767，无符号的范围是0到65535。   
  
MEDIUMINT[(M)] [UNSIGNED] [ZEROFILL]   
一个中等大小整数。有符号的范围是-8388608到8388607，无符号的范围是0到16777215。   
  
INT[(M)] [UNSIGNED] [ZEROFILL]   
一个正常大小整数。有符号的范围是-2147483648到2147483647，无符号的范围是0到4294967295。   
  
INTEGER[(M)] [UNSIGNED] [ZEROFILL]   
这是INT的一个同义词。   
BIGINT[(M)] [UNSIGNED] [ZEROFILL]   
一个大整数。有符号的范围是-9223372036854775808到9223372036854775807，无符号的范围是0到  
18446744073709551615。注意，所有算术运算用有符号的BIGINT或DOUBLE值完成，因此你不应该使用大于9223372036854775807（63位)的有符号大整数，除了位函数！注意，当两个参数是INTEGER值时，-、+和*将使用BIGINT运算！这意味着如果你乘2个大整数(或来自于返回整数的函数)，如果结果大于9223372036854775807，你可以得到意外的结果。一个浮点数字，不能是无符号的，对一个单精度浮点数，其精度可以是<=24，对一个双精度浮点数，是在25 和53之间，这些类型如FLOAT和DOUBLE类型马上在下面描述。FLOAT(X)有对应的FLOAT和DOUBLE相同的范围，但是显示尺寸和小数位数是未定义的。在MySQL3.23中，这是一个真正的浮点值。在更早的MySQL版本中，FLOAT(precision)总是有2位小数。该句法为了ODBC兼容性而提供。  
  
FLOAT[(M,D)] [ZEROFILL]   
一个小(单精密)浮点数字。不能无符号。允许的值是-3.402823466E+38到-1.175494351E-38，0 和1.175494351E-38到3.402823466E+38。M是显示宽度而D是小数的位数。没有参数的FLOAT或有<24 的一个参数表示一个单精密浮点数字。   
DOUBLE[(M,D)] [ZEROFILL]   
一个正常大小(双精密)浮点数字。不能无符号。允许的值是-1.7976931348623157E+308到-2.2250738585072014E-308、 0和2.2250738585072014E-308到1.7976931348623157E+308。M是显示宽度而D是小数位数。没有一个参数的DOUBLE或FLOAT(X)（25 < = X < = 53）代表一个双精密浮点数字。   
DOUBLE PRECISION[(M,D)] [ZEROFILL]   
REAL[(M,D)] [ZEROFILL]   
这些是DOUBLE同义词。   
DECIMAL[(M[,D])] [ZEROFILL]   
一个未压缩(unpack)的浮点数字。不能无符号。行为如同一个CHAR列：“未压缩”意味着数字作为一个字符串被存储，值的每一位使用一个字符。小数点，并且对于负数，“-”符号不在M中计算。如果D是0，值将没有小数点或小数部分。DECIMAL值的最大范围与DOUBLE相同，但是对一个给定的DECIMAL列，实际的范围可以通过M和D的选择被限制。如果D被省略，它被设置为0。如果M被省掉，它被设置为10。注意，在MySQL3.22里，M参数包括符号和小数点。   
  
  
NUMERIC(M,D) [ZEROFILL]   
这是DECIMAL的一个同义词。 DATE   
一个日期。支持的范围是'1000-01-01'到'9999-12-31'。MySQL以'YYYY-MM-DD'格式来显示DATE值，但是允许你使用字符串或数字把值赋给DATE列。   
DATETIME   
一个日期和时间组合。支持的范围是'1000-01-01 00:00:00'到'9999-12-31 23:59:59'。MySQL以'YYYY-MM-DD HH:MM:SS'格式来显示DATETIME值，但是允许你使用字符串或数字把值赋给DATETIME的列。   
TIMESTAMP[(M)]   
一个时间戳记。范围是'1970-01-01 00:00:00'到2037年的某时。MySQL以YYYYMMDDHHMMSS、YYMMDDHHMMSS、YYYYMMDD或YYMMDD格式来显示TIMESTAMP值，取决于是否M是14（或省略)、12、8或6，但是允许你使用字符串或数字把值赋给TIMESTAMP列。一个TIMESTAMP列对于记录一个INSERT或UPDATE操作的日期和时间是有用的，因为如果你不自己给它赋值，它自动地被设置为最近操作的日期和时间。你以可以通过赋给它一个NULL值设置它为当前的日期和时间。   
TIME   
一个时间。范围是'-838:59:59'到'838:59:59'。MySQL以'HH:MM:SS'格式来显示TIME值，但是允许你使用字符串或数字把值赋给TIME列。   
YEAR[(2|4)]   
一个2或4位数字格式的年(缺省是4位)。允许的值是1901到2155，和0000（4位年格式），如果你使用2位，1970-2069( 70-69)。MySQL以YYYY格式来显示YEAR值，但是允许你把使用字符串或数字值赋给YEAR列。（YEAR类型在MySQL3.22中是新类型。）   
CHAR(M) [BINARY]   
一个定长字符串，当存储时，总是是用空格填满右边到指定的长度。M的范围是1 ～ 255个字符。当值被检索时，空格尾部被删除。CHAR值根据缺省字符集以大小写不区分的方式排序和比较，除非给出BINARY关键词。NATIONAL CHAR（短形式NCHAR)是ANSI SQL的方式来定义CHAR列应该使用缺省字符集。这是MySQL的缺省。CHAR是CHARACTER的一个缩写。   
[NATIONAL] VARCHAR(M) [BINARY]   
一个变长字符串。注意：当值被存储时，尾部的空格被删除(这不同于ANSI SQL规范)。M的范围是1 ～ 255个字符。 VARCHAR值根据缺省字符集以大小写不区分的方式排序和比较，除非给出BINARY关键词值。 VARCHAR是CHARACTER VARYING一个缩写。   
TINYBLOB 　   
TINYTEXT   
一个BLOB或TEXT列，最大长度为255(2^8-1)个字符。   
BLOB   
TEXT   
一个BLOB或TEXT列，最大长度为65535(2^16-1)个字符。   
MEDIUMBLOB 　   
MEDIUMTEXT   
一个BLOB或TEXT列，最大长度为16777215(2^24-1)个字符。   
LONGBLOB 　   
LONGTEXT   
一个BLOB或TEXT列，最大长度为4294967295(2^32-1)个字符。   
ENUM('value1','value2',...)   
枚举。一个仅有一个值的字符串对象，这个值式选自与值列表'value1'、'value2', ...,或NULL。一个ENUM最多能有65535不同的值。  
SET('value1','value2',...)   
一个集合。能有零个或多个值的一个字符串对象，其中每一个必须从值列表'value1', 'value2', ...选出。一个SET最多能有64个成员。
 




