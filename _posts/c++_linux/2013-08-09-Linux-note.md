---
layout: post
title: Linux随手记
category: c++_linux
tags: Linux
description: 随手记Linux小问题
---

### 安装vmware tools

1. 如果直接点虚拟机中的安装不行的话，在CD-ROM虚拟光驱中选择使用ISO镜像，找到VMWARE TOOLS 安装文件，如C:\program\VMware\VMware Workstation\Programs\linux.iso
当然这个ISO是你安装VMware workstation 的目录下的Linux.iso，不是你的Linux OS 镜像文件。VMware Tools一般都在这个文件里。

2. 然后再在虚拟机菜单栏中点击 虚拟机-> 安装 VMWARE TOOLS 子菜单,会弹出对话框，点击"确认" 安装

3. 一般可以看到光驱直接点进去能发现安装文件了。
如果没有那就挂载光驱：Mount -t iso9660 /dev/cdrom /mnt           加载CDROM设备，这是如果进入/mnt 目录下，你会发现一个文件：
VMwareTools-8.8.4-743747.tar.gz                  这个就是VMwareTools的Linux软件包，也是我们刚才使用的WinISO打开的Liunx.ISO
有的虚拟机上估计执行mount /dev/cdrom /mnt/cdrom
如果提示如下错误，挂载点不存在。，[root@localhost /]#mount /dev/cdrom /mnt/cdrom
mount: mount point /mnt/cdrom dose not exist
请直接执行此命令：     mount /dev/cdrom /opt
cd /opt
或者应该可以使用自动挂载，直接进入
cd /misc/cd

4. copy 此文件到临时文件夹
 cp /mnt/mVMwareTools-8.8.4-743747.tar.gz /tmp

5. 卸载CDROM，执行 umount /dev/cdrom

6. 进入tmp文件目录并解压此文件包
   cd /tmp
　tar -xvf VMwareTools-9.6.0-1294478.tar.gz(解压文件，注意，这里的文件名是你自己桌面上那个.gz文件的名称，版本有差异，文件名也不同，不过后缀都是.gz，按照自己的来)
这时候应该多了一个文件夹，下面执行
cd vmware-tools-distrib (进入解压出来的文件夹vmware-tools-distrib，文件夹名按照你自己的来)
然后运行就可以了：   sudo ./vmware-install.pl（sudo 分配权限安装）
然后输入密码，一路回车，就安装完了！

### 命令，做一下记录！
tar
格式： tar [选项] [文件目录列表]
功能： 对文件目录进行打包备份
选项：
-c 建立新的归档文件
-r 向归档文件末尾追加文件
-x 从归档文件中解出文件
-O 将文件解开到标准输出
-v 处理过程中输出相关信息
-f 对普通文件操作
-z 调用gzip来压缩归档文件，与-x联用时调用gzip完成解压缩
-Z 调用compress来压缩归档文件，与-x联用时调用compress完成解压缩

1.用tar打包一个目录下的文件:＃tar -cvf /mnt/lgx/a1.doc
生成一个以.tar为扩展名的打包文件

2.用tar解开打包文件：＃tar -xvf /mnt/lgx/a1.doc.tar
通常情况下，tar打包与gzip（压缩）经常联合使用。方法：
首先用tar打包，如：＃tar -cvf /mnt/lgx/a1.doc （产生a1.doc.tar文件）
然后用gzip压缩a1.doc.tar文件，如：＃gzip /mnt/lgx/a1.doc.tar （产生a1.doc.tar.gz文件）

3.解压a1.doc.tar.gz文件
方法1：
＃gzip -dc /mnt/lgx/a1.doc.tar.gz （产生a1.doc.tar文件）
＃tar -xvf /mnt/lgx/a1.doc.tar （产生a1.doc文件）
这两次命令也可使用管道功能，把两个命令合二为一：
＃gzip -dc /mnt/lgx/a1.doc.tar.gz | tar -xvf

方法2：使用tar提供的自动调用gzip解压缩功能
＃tar -xzvf /mnt/lgx/a1.doc.tar.gz
经过tar打包后，也可用compress命令压缩（注：gzip比compress压缩更加有效），产生一个以.tar.Z的文件，在解包时，可先用 “uncompress 文件名”格式解压，然后用“tar -xvf 文件名”解包。也可直接调用“tar -Zxvf 文件名”解包。

### 安装SSH服务
1、首先保证你的网络配好能拼通ubuntu，再查看ssh服务情况。
ubuntu默认并没有安装ssh服务，如果通过ssh链接ubuntu，需要自己手动安装ssh-server。
判断是否安装ssh服务：
1可以通过如下命令进行：    zcw@zcw-VM-Ubuntu:~$ ssh localhost
　　　　　　　　　　      　ssh: connect to host localhost port 22: Connection refused  //所示，表示没有还没有安装，
2检查安装系统时是否已经安装SSH服务端软件包:      zcw@zcw-VM-Ubuntu:~$rpm -qa|grep openssh            // 若显示结果中包含openssh-server-*,则说明已经安装,直接启动

2、安装SSH
通过apt安装，命令如下：
　　　zcw@zcw-VM-Ubuntu:~$ sudo apt-get install openssh-server  
 　　　  sshd服务就可以了(service sshd start).(其中*的内容是该包的版本,一般为3.5p1-6)
  　　　若无任何显示,或显示中不包含openssh-server-*则说明没有安装SSH服务端软件如果apt命令不行：出现了Package has no installation candidate的问题，如： 
  apt-get install <packagename>
Reading package lists... Done
Building dependency tree... Done
Package aptitude is not available, but is referred to by another package.
This may mean that the package is missing, has been obsoleted, or
is only available from another source
E: Package <packagename> has no installation candidate
解决方法如下：
`# apt-get update`
`# apt-get upgrade`
`# apt-get install <packagename>`
这样就可以正常使用apt-get了
添加第三方地址：
sudo add-apt-repository "deb http://archive.canonical.com/ lucid partner"
sudo apt-get update
3、启动SSH服务： 
zcw@zcw-VM-Ubuntu:~$ sudo /etc/init.d/ssh start  
启动后，可以通过如下命令查看服务是否正确启动
zcw@zcw-VM-Ubuntu:~$ ps -e|grep ssh   
6212 ?        00:00:00 sshd  
如上表示启动ok。注意，ssh默认的端口是22，可以更改端口，更改后先stop，然后start就可以了。
改配置在/etc/ssh/sshd_config下，如下所示。 
zcw@zcw-VM-Ubuntu:~$ vi /etc/ssh/sshd_config   
最后，你就应该可以putty连接成功了。（用ifconfig查看一下你的Ubuntu的ip地址）。
 
## 日常小问题
一、修改完主机名后在执行sudo命令时，
        会提示sudo: 无法解析主机。在网上搜了下，找到了解决方法：
        $  sudo vim /etc/hosts
           找到如下行： 127.0.1.1 XXX                                修改为：127.0.1.1 （修改后的主机名）