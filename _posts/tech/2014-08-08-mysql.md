---
layout: post
title: 用MySQL connector/C++链接MySQL数据库
category: 技术
tags: MySQL
keywords: MySQL
description:
---

首先去MySQL官网下载MySQL connector/C++
http://dev.mysql.com/downloads/connector/cpp/
下载windows32位非安装版。目前的版本是Connector/C++ 1.1.4。
Windows (x86, 32-bit), ZIP Archive (mysql-connector-c++-noinstall-1.1.4
将整个包解压到项目文件夹下的的源文件目录。文件夹名字太长，将“mysql-connector-c++-noinstall-1.0.5-win32”改为“mysql”。
下面要配置vs2008的环境。
1. 项目属性页->C/C++->General->Additional Include Directories。将mysql/include目录和mysql/include/cppconn目录添加进去。
2. 项目属性页->Linker->General->Additional Library Directories。将mysql/lib目录添加进去。
3. 项目属性页->Linker->Input->Additional Dependencies。添加这两项mysqlcppconn.lib，mysqlcppconn-static.lib（mysql/lib目录下的两个.lib文件）
4. 将mysql/lib下的mysqlcppconn.dll文件复制到windows/system32文件夹下。
环境配置完毕。
 
在连接数据库之前，先建立一张表。 （其实这些可以在代码中完成，我这样是为了让测试代码尽可能简练易查错）
打开控制台，输入mysql -u root -p，输入密码。
查看当前已有的数据库。（SQL语句末尾加上';'表示立即执行当前语句。）
mysql> show databases;
创建数据库
mysql> create database test;
使用数据库（这句不能加分号）
mysql> use test
查看已有的表
mysql> show tables;
创建表
mysql> create table testuser ( id INT, name CHAR(20));
插入数据
mysql> insert into testuser(id, name) values(1001, 'google');
mysql> insert into testuser(id, name) values(1002, 'kingsoft');
mysql> insert into testuser(id, name) values(1003, 'firefox');

现在在C++中查询这些数据


	#include "stdafx.h"  
	#include <mysql_connection.h>  
	#include <mysql_driver.h>  
	#include <statement.h>  
	using namespace sql;  
	using namespace std;  
	void RunConnectMySQL()   
	{  
		mysql::MySQL_Driver *driver;  
		Connection *con;  
		Statement *state;  
		ResultSet *result;  
		// 初始化驱动  
		driver = sql::mysql::get_mysql_driver_instance();  
		// 建立链接  
		con = driver->connect("tcp://127.0.0.1:3306", "root", "123");  
		state = con->createStatement();  
		state->execute("use test");  
		// 查询  
		result = state->executeQuery("select * from testuser where id < 1002");  
		// 输出查询  
		while(result->next())  
		{  
			int id = result->getInt("ID");  
			string name = result->getString("name");  
			cout << id << " : " << name << endl;  
		}  
		delete state;  
		delete con;  
	}  
	int _tmain(int argc, _TCHAR* argv[])  
	{  
		RunConnectMySQL();  
		getchar();  
		return 0;  
	}  

（可能会报一些无法打开XXXX.h，自行查找添加）


看起来很方便的样子~

另外，我在MySQL官网上找C++的API时候发现常用的API有两个。一个是很成熟的MySQL++，据说用了很多年了经历了若干变化，深受好评；另一个就是这里介绍的MySQL Connector/C++（之前我就弄混了，后来发现这两个不是同一个东西），近两年才出的，模仿JDBC做的，封装得很方便使用。

##还有就是用ODBC链接Mysql。

