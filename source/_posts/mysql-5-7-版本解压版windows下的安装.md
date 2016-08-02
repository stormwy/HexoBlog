---
title: mysql 5.7 版本解压版windows下的安装
date: 2016-08-01 16:08:32
categories: 数据库
tags: mysql				
---
mysql 5.7解压版windows安装有点琐碎，在此记录一下。
## 安装过程
### 1.解压、配置path     
解压到想要安装的目录：`D:\develop\mysql-5.7.13-winx64`      
将位置`D:\develop\mysql-5.7.13-winx64\bin`配置到环境变量path中。
### 2.创建配置文件      
将my-default.ini复制一份，改名为my.ini作为mysql配置文件，并且去掉my.ini里面的`basedir`、`datadir`注释，并设置相应路径        
```
# set basedir to your installation path
basedir = D:\develop\mysql-5.7.13-winx64
# set datadir to the location of your data directory
datadir = D:\develop\mysql-5.7.13-winx64\data
```
### 3.数据初始化       
打开命令行，运行
```
mysqld --initialize-insecure
```
这样就完成data目录初始化。采用这种方式初始化，root用户是没有设置密码的，
后面需要进行密码的设置。
#### 4.安装mysql服务     
```
mysqld --install
```
### 5.运行、停止mysql        
```
net start mysql
net stop mysql
```
### 6.用户密码设置
首先进入mysql，
```
mysql -u root --skip-password
```
运行下面语句进行用户密码设定：
```
 ALTER USER 'root'@'localhost' IDENTIFIED BY 'new_password';
```
## 可能遇到的问题
### 1.运行“net start mysql”时提示：发生系统错误 2		
这个问题一般是在data目录初始化之前，先进行了mysql服务安装引起的。		
解决方式是，到`bin`目录运行:		
```
mysqld --remove //移除服务
mysqld --install //重新安装服务
```
然后重新运行就行。

### 参考资料
官方安装文档:[Installing MySQL on Microsoft Windows Using a noinstall Zip Archive](http://dev.mysql.com/doc/refman/5.7/en/windows-install-archive.html)     
另外一篇写得很完整的安装文档:http://blog.csdn.net/tianyan5/article/details/51789433)

