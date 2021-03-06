## 1. CENTOS: 增加SWAP的大小

### 第一步：关闭SWAP

` sudo swapoff -a`

### 第二步：把当前的SWAP文件增大

 `sudo dd if=/dev/zero of=/swapfile bs=1M count=1024`

> bs指的是Block Size，就是每一块的大小。这里的例子是1M，意思就是count的数字，是以1M为单位的。
counter是告诉程序，新的swapfile要多少个block。这里是1024，就是说，新的swap文件是1G大小。

### 第三步：把增大后的文件变为swap文件。

`sudo mkswap /swapfile`

### 第四步：重新打开swap

` sudo swapon /swapfile `

### 第五步：让swap在启动的时候，自动生效。打开/etc/fstab文件

`sudo vim /etc/fstab`


### 第六步：最后一行，加上以下命令。然后保存。

`/swapfile swap swap defaults 0 0`


完成。


## 2. 安装mysql8.0
### 1. Enable the MySQL 8.0 repository with the following command:
```
sudo yum localinstall https://dev.mysql.com/get/mysql80-community-release-el7-1.noarch.rpm
```
### 2. Install MySQL 8.0 package with yum:
```
sudo yum install mysql-community-server
```

### start mysql
```
sudo systemctl enable mysqld
sudo systemctl start mysqld
```
### 查看默认密码
在启动MySQL服务的时候，主要会发生以下4件事

* MySQL Server初始化并启动起来；
* MySQL的data文件夹中生成SSL证书和key文件；
* 密码验证组件被安装并且生效；
* 创建一个超级管用户'root'@'localhost‘。超级用户设置的密码被保存在错误日志文件中，可以通过以下命令查看：
```
sudo grep 'temporary password' /var/log/mysqld.log
```
### 修改密码
```
ALTER USER 'root'@'localhost' IDENTIFIED BY '{你的密码}';
```
### 添加用户 
> % 允许远程访问
```
CREATE USER 'jeffrey'@'%' IDENTIFIED BY 'password';
The
```
[参考链接含5.7](https://linuxize.com/post/install-mysql-on-centos-7/)
