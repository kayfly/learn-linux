# learn-linux
学习linux，里面有一些练习过程中的练手项目

h是向左移动光标，向下，向上，向右分别是j,k,l
w是写入，:q是退出，wq退出并保存，q!强制退出。
尝试修改。

cat XXX  
代表列出 XXX 文件的内容



——————————————
ls list 列出目录下文件
cd changedir 切换目录
pwd 列出当前的路径
rm 删除
mv 移动文件或文件夹
——————————————
apt 所有的程序安装管理  理同termux
apt install  xxx  git
apt remove
apt update #更新包管理的数据库，并不更新包
apt upgrade #更新包

apt install git -y
apt remove git -y

npm install
npm uninstall
npm update
#常用软件  vim git lrzsz
apt install vim git lrzsz -y

#权限
chmod 777 normal.sh

### 简单命令

删除：rm / -rf

解压：unzip（zip文件）   tar -xzf filename.tar.gz(tar.gz文件)

上传下载：install lrzsz 然后 rz 上传 sz下载



## 日常遇到的问题及解决

## 1， 安装Apache参考本文：https://www.linuxidc.com/Linux/2018-05/152261.htm

**出现**：

a, 80端口被占用，提示：Job for httpd.service failed because the control process exited with error code

（可先跳过这里：查看端口占用情况：netstat -antlp | grep 80

caddy服务占用了，想起来之前搭建梯子的时候用到的

使用v2ray status查看caddy运行情况

这里先停止caddy服务，放出80端口

sudo systemctl start httpd

再次启动apache服务，访问服务器地址，成功运行

停止couchdb服务

systemctl stop couchdb

非后台启动couchdb

sudo -i -u couchdb /opt/couchdb/bin/couchdb

关于停止，开始，重启服务的操作详见：https://blog.csdn.net/qq_39564555/article/details/88413634

)

**解决**：

a.1, find /etc/httpd/ -name *conf（查找httpd.conf文件的位置）

a.2, vim /etc/httpd/conf/httpd.conf（编辑配置文件，找到listen监听端口位置进行修改）

## 2，安装python2.7：https://www.jianshu.com/p/c4dcad89a9f4

tar -xf Python-2.7.11.tar

进入安装文件目录进行安装

cd Python-2.7.11

./configure

make

make install

## 这是在安装couchdb过程中遇到的问题，需要安装apache环境，还需要安装python2.7，一堆错误

遇到了安装python2.7后 yum后命令无法使用得情况，这里vim /usr/bin/yum，第一行的python后加上2.7为python2.7即可解决

出现：Error: Package: couchdb-2.3.1-1.el7.x86_64 (bintray--apache-couchdb-rpm)
           Requires: python-progressbar

尝试：安装python-progressbar

先安装pip

遇到了找不到python-pip源的问题，这里需要手动开启epel源：vim /etc/yum.repos.d/epel.repo

enable：1

卧槽，真的要爆炸了，又出现了 No module named urlgrabber.grabber的问题

```
vim /usr/libexec/urlgrabber-ext-down
把第一行的python改成和/usr/bin/yum中一样的就可以了python2.7
```

继续

yum install -y python-pip

```
sudo yum -y install epel-release && yum install couchdb
```

这次终于成功了

![1565360752494](C:\Users\xipudata\AppData\Roaming\Typora\typora-user-images\1565360752494.png)

真的是一波三折~（但此时还是无法顺利运行couchdb，现在请返回去看可跳过部分）