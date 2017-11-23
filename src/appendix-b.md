# 附录-乙 测试平台vagrant部署
# 制作基于centos6.7和xampp7.0.1的vagrant box

已制作下载地址：http://pan.baidu.com/s/1o6Zq5zc

参考网页：
+ http://thornelabs.net/2013/11/11/create-a-centos-6-vagrant-base-box-from-scratch-using-virtualbox.html
+ http://my.oschina.net/bubifengyun/blog/550066
+ http://www.vagrantbox.es/
+ https://atlas.hashicorp.com/boxes/search?utm_source=vagrantcloud.com&vagrantcloud=1

已有较多的制作教程，本例讲述在 Ubuntu 麒麟下的制作过程。

# 一、软件准备

+ centos6.7 安装包，本次安装采用的是DVD1包，http://www.centoscn.com/CentosSoft/iso/2015/0813/6001.html
+ virtualbox 5.0.12及其扩展包，https://www.virtualbox.org/wiki/Downloads，
+ vagrant 安装包，https://www.vagrantup.com/downloads.html
+ xampp 7.0.1,https://www.apachefriends.org/download.html

# 二、准备工作

## 1、virtualbox 安装

本文下载的是deb文件，下面主要讲述命令行安装方式。

```
sudo dpkg -i /path/to/virtualbox.deb
```

安装完成后，应该可以在终端输入`virtualbox`启动virtualbox软件。

关闭virtualbox后，双击下载的virtualbox扩展包，可以直接安装成功。

## 2、vagrant 安装

下载最新包安装即可。

```
sudo dpkg -i /path/to/vagrant.deb
```

上面两步也可以跳过，直接使用命令行如下安装。


```
sudo apt-get install vagrant virtualbox -y
```
切记给virtualbox安装扩展支持。

# 三、安装centos

## 1、预备安装

+ 打开虚拟机virtualbox，New新建主机命名centos,
+ Type类型选择Linux,
+ Version版本选择Red Hat(64bit),
+ Memory size内存大小可以设置为512MB或者更多，
+ Hard drive 硬盘选择Create a virtual hard drive now新建硬盘，点击创建，
+ File Location硬盘文件地址选择默认，或者其他位置，看你磁盘空间而定，
+ File size硬盘大小默认8G足够，如有更多需求，你可以调大；
+ Hard Drive file type硬盘类型，选择VDI
+ Storage on physical hard drive 驱动存储方式, 选择 Dynamically allocated动态方式, 点击Create创建；
+ 现在打开Settings 设置，在存储里找到Controller：IDE，选择你下载的centos-6.7-x86-64-bin-DVD1.iso
+ 在声音和端口内关闭声音和USB驱动。
+ 点击确定

## 2、安装系统

选择virtualbox的centos，点击启动即可。
+ 建议安装过程中语言之类的选择English，如果需要可以选择中文简体。
+ root密码设置为vagrant
+ 时区选择Asia/Shanghai，时间不选UTC。
+ 最后安装类型选择最小化安装。
+ 其他选择默认。
安装完毕后重启。

## 3、配置系统（手动版）

本小节为配置的手动版，下面还有自动版（Kickstart Profile Installation）。两者选择其一即可。

下面非特殊说明，用户均为root。登录系统。用户名和密码为root,vagrant

### 3.1 启动网卡

系统默认不启动网卡的，所以要先启动他。

```
ifup eth0
```

### 3.2 安装必须的一些软件包

```
yum install -y openssh-clients man git vim wget curl ntp gcc
```
其中`vim`自认为不需要，`gcc`是为后续安装虚拟机系统guest os内部的virtualbox扩展包所用。

如果不可以上网，确认你虚拟机网络借口的配置方式是否正确，试试桥接或NAT方式，如果实在不行，请避免选用最小安装包的.iso文件，选择正确的安装包。

### 3.3 配置一些启动默认项

+ 启动ntpd服务

```
chkconfig ntpd on
```

+ 启动sshd服务

```
chkconfig sshd on
```

+ 设置SELinux允许

```
sed -i -e 's/^SELINUX=.*/SELINUX=permissive/' /etc/selinux/config
```

### 3.4 创建vagrant用户及其相关内容

```
useradd vagrant
mkdir -m 0700 -p /home/vagrant/.ssh
curl https://raw.githubusercontent.com/mitchellh/vagrant/master/keys/vagrant.pub >> /home/vagrant/.ssh/authorized_keys
chmod 600 /home/vagrant/.ssh/authorized_keys
chown -R vagrant:vagrant /home/vagrant/.ssh
sed -i 's/^\(Defaults.*requiretty\)/#\1/' /etc/sudoers
echo "vagrant ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
```

考虑到一般不会对vagrant做太多改动，故采用默认的做法。
上述命令详细解释及说明见：http://thornelabs.net/2013/11/11/create-a-centos-6-vagrant-base-box-from-scratch-using-virtualbox.html

### 3.5 配置网卡参数

编辑`/etc/sysconfig/network-scripts/ifcfg-eth0`，部分参数如下：

```
DEVICE=eth0
TYPE=Ethernet
ONBOOT=yes
NM_CONTROLLED=no
BOOTPROTO=dhcp
```

重启电脑进入 4、安装虚拟机操作系统centos的virtualbox扩展。

## 3、配置系统（自动版）

详见参考文献：http://thornelabs.net/2013/11/11/create-a-centos-6-vagrant-base-box-from-scratch-using-virtualbox.html

<table>
Kickstart Profile Installation
I used this Kickstart Profile to automate the build.
When the CentOS boot menu appears, highlight Install or upgrade an existing system, hit the Tab key to bring up the anaconda boot line, and append the following:

```
noverifyssl ks=https://raw.githubusercontent.com/jameswthorne/kickstart-profiles/master/centos-6-x86_64-vagrant-box.txt
```

Hit the Enter key and wait for the installation to finish.
</table>

说人话就是：

在centos系统启动菜单里，选择Install or upgrade an existing system，点击Tab键，在后面添加如下内容。

```
noverifyssl ks=https://raw.githubusercontent.com/jameswthorne/kickstart-profiles/master/centos-6-x86_64-vagrant-box.txt
```

回车，等待安装完成。

重启电脑进入 4、安装虚拟机操作系统centos的virtualbox扩展。

## 4、安装虚拟机操作系统centos的virtualbox扩展

打开virtualbox某个虚拟机时，最上面菜单栏有个`设备`>`安装增强功能`。如果你电脑联网，virtualbox一般会自动帮你下载好该光盘并挂载在你的虚拟机上。
下面假设该光盘已经在你电脑上了。实在无法解决的，可以自行百度下载。

root用户进入到虚拟机centos中

在/root文件夹下新建一个文件cdromtmp

```
mkdir /root/cdromtmp
```

把光盘挂载到/root/cdromtmp下

```
mount /dev/cdrom /root/cdromtmp
```

注意，上面有可能是`/dev/cdrom1`或者其他，可以使用命令`ls /dev/cdrom*`查看，确实是否存在。

执行安装该扩展功能。

```
/root/cdromtmp/VBoxLinuxAdditions.run
```

找到类似的VBoxLinuxAdditions.run.run文件即可。有时候会出现缺少 `kernel-devel-xxx`的问题，按照提示安装。
最后可能会有opengGL的相关东西安装失败，不影响操作，可以继续。
这样就安装成功了。建议重启电脑。

# 四、安装xampp

centos系统一般默认是开通ssh,22端口的。如果可以查看centos的IP地址，不妨设为192.168.1.201，可以采用ssh或者sftp跟centos联通。
下面假设可以访问该虚拟机。

```
ssh root@192.168.1.201
```

## 1、开通8080,80,22端口

**下面如果没有特别说明，均为root用户在ssh里操作。**

centos 6.7依旧采用的是iptables管理端口。跟centos7不同。
编辑文件，

```bash
vi /etc/sysconfig/iptables
```

加入如下内容，一般22端口默认开通了，其他端口可以类似添加开通。

```
-A INPUT -m state –state NEW -m tcp -p tcp –dport 22 -j ACCEPT
-A INPUT -m state –state NEW -m tcp -p tcp –dport 80 -j ACCEPT
-A INPUT -m state –state NEW -m tcp -p tcp –dport 8080 -j ACCEPT
```

保存退出，重启查看iptables

```bash
/etc/init.d/iptables restart
/etc/init.d/iptables status
```

## 2、安装xampp

通过sftp把其他电脑上的xampp.run文件复制过来。

```bash
sftp root@192.168.1.201
#跳过代码部分
sftp put /path/to/xampp.run ./
```

这样把xampp.run文件复制到/root文件夹下了。

如果xampp.run没有执行权限，需要添加可以执行权限。

```bash
chmod u+x ./xampp.run
```
下面安装xampp.run文件。

```bash
./xampp.run
```

记住选择非开发模式。默认安装在/opt/lampp文件夹。

可以顺利安装完成。

可以在/opt/lampp/htdocs/下新建一个文件夹www,并让所有人对该文件夹操作。

```
mkdir /opt/lampp/htdocs/www
chmod -m 0777 -p /opt/lampp/htdocs/www
```


## 3、xampp加入开机自启动

首先在/etc/init.d下添加一个xampp启动脚本

```bash
vi /etc/init.d/xampp.sh
```

添加以下内容

```bash
#!/bin/sh
/opt/lampp/lampp start
```

保存退出,添加自启动

```bash
vi /etc/rc.d/rc.local
```

加入以下代码

```bash
sh /etc/init.d/xampp.sh
```

保存退出
注意要给上面两个文件加上执行权限。

```bash
chmod u+x /etc/init.d/xampp.sh
chmod u+x /etc/rc.d/rc.local
```

## 4、配置xampp可以在同局域网下使用phpmyadmin

编辑文件，

```bash
vi /opt/lampp/etc/extra/httpd-xampp.conf
```

修改为如下情况

```
<LocationMatch "^/(?i:(?:xampp|security|licenses|phpmyadmin|webalizer|server-status|server-info))">
#       Require local
        Require all granted
        ErrorDocument 403 /error/XAMPP_FORBIDDEN.html.var
</LocationMatch>

```
注释掉只能本地访问功能，增加外网访问能力。
保存退出。

## 5、编辑文件`/opt/lampp/etc/httpd.conf`

```
vi /opt/lampp/etc/httpd.conf
```

在文中搜索`httpd-vhost.conf`,会找到

```bash
#Include etc/extra/httpd-vhosts.conf
```

取消该行注释。

在文中搜索`80`,会找到

```bash
Listen 80
```

改为

```bash
Listen 80
Listen 8080
```

### 6、编辑/opt/lampp/etc/extra/httpd-vhosts.conf

```bash
vi /opt/lampp/etc/extra/httpd-vhosts.conf
```

加入如下内容，可以类似修改。

```
<VirtualHost *:80>
    ServerAdmin bubifengyun@sina.com
    DocumentRoot "/opt/lampp/htdocs/www"
    ServerName personshakehand.lxfive.com
    ServerAlias www.personshakehand.lxfive.com
    ErrorLog "logs/personshakehand-error_log"
    CustomLog "logs/personshakehand-access_log" common
</VirtualHost>

<VirtualHost *:8080>
    ServerAdmin bubifengyun@sina.com
    DocumentRoot "/opt/lampp/htdocs"
    ServerName backend.personshakehand.lxfive.com
    ServerAlias www.backend.personshakehand.lxfive.com
    ErrorLog "logs/backend-personshakehand-error_log"
    CustomLog "logs/backend-personshakehand-access_log" common
</VirtualHost>
```

# 五、清理现场

在虚拟机中，去除一些不需要的日志信息等。

```
rm -f /etc/udev/rules.d/70-persistent-net.rules
yum clean all
rm -rf /tmp/*
rm -f /var/log/wtmp /var/log/btmp
history -c
shutdown -h now
```

删掉虚拟机的光盘驱动。

打开存储，可以看到有光盘标志的地方，选中他，在下面有删除按钮，选择删除他。

# 六、创建 create vagrant box

退出到主机，非虚拟机。

```
vagrant package --output centos-6.7-x64.box --base centos
```

添加vagrant box

```
vagrant box add centos-6.7-x64 centos-6.7-x64.box
```

跳转到工作文件夹

```
cd /opt/lampp/htdocs/www
```

初始化vagrant

```
vagrant init centos-6.7-x64
```

修改Vagrantfile,这时会在当前文件夹下看到Vagrantfile文件，其中部分内容如下。

```
  config.vm.network "public_network", ip: "192.168.1.201"
  config.vm.synced_folder "./", "/opt/lampp/htdocs/www/"
```

确保在局域网其他电脑也可以访问测试。并让当前工作文件夹和虚拟机服务器centos对应的文件夹可以访问。

启动vagrant，默认在当前文件夹下，

```
vagrant up
```

会弹出选择网卡等信息，如果不出意外，应该是可以正常启动了。


# 七、备注

+ 本文制作的centos-6.7-x64.box在百度云盘提供下载。
+ 在制作过程中对MySQL的用户和密码都进行了修改，分别为test,test

# 使用说明：

+ 假设你已经安装好了virtualbox,vagrant,且你的virtualbox支持64位操作系统。
+ 下载好centos-6.7-x64.box
+ 进入到你的工作项目根目录，不妨设为/opt/lampp/htdocs/www
+ 安装该虚拟机

```
vagrant box add <your-webserver-name> /path/to/centos-6.7-x64.box
vagrant init <your-webserver-name>
vagrant up
```

+ 如果你的虚拟机允许正常，关闭vagrant

```
vagrant halt
```

+ 可以编辑当前目录下的`Vagrantfile`文件，类似如下修改。

```
  config.vm.network "public_network", ip: "192.168.1.201"
  config.vm.synced_folder "./", "/opt/lampp/htdocs/www/"
```

+ 使用xampp,在/opt/lampp/htdocs/www下新建项目文件夹，
+ 在同一局域网其他电脑上，查看虚拟机IP地址对应的网站。


有问题欢迎在下面留言，或者发送邮件到bubifengyun@sina.com
