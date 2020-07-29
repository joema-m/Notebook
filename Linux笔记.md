# 记录平时遇到的linux问题



## 虚拟机中不能复制粘贴

```shell
sudo apt-get autoremove open-vm-tools
sudo apt-get install open-vm-tools-desktop
sudo reboot
```



## 修改apt源

```shell
sudo mv /etc/apt/sources.list   /etc/apt/sources.list.bak

sudo vim /etc/apt/sources.list

# 添加以下内容
deb http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse

deb-src http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse

deb http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse

deb-src http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse

deb http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse

deb-src http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse

deb http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse

deb-src http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse

deb http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse

deb-src http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse


#更新apt-get
sudo apt-get update

sudo apt-get upgrade
```



## 修改pip源

在用户目录下创建*.pip/pip.conf*文件（Windows ：pip.ini）

```shell
mkdir .pip
cd .pip
vim pip.conf

[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
trusted-host = pypi.tuna.tsinghua.edu.cn
```



## 防火墙配置

在RHEL 7系统中， firewalld防火墙取代了 iptables防火墙。它们都只是用来定义防火墙策略的防火墙管理工具而已，或者说，它们只是一种服务。

它们都只是用来定义防火墙策略的防火墙管理工具而已，或者说，它们只是一种服务。 iptables服务会把配置好的防火墙策略交由内核层面的 netfilter网络过滤器 来处理，而 firewalld服务则是把配置好的防火墙策略交由内核层面的 nftables包过滤框架来处理。

![img](./img/iptables.jpg)

例如，添加一条开放某个端口的规则：

```shell
iptables -A INPUT -p tcp --dport 2048 -j ACCEPT
```

注意，这样添加的只是临时规则，重启iptables服务后就会失效

```shell
# 这样才会添加到规则保存文件中
service iptables save

# 规则保存文件在这里
vim /etc/sysconfig/iptables
```

[这里有详细教程](https://www.91yun.co/archives/1690)



## 根据域名字段屏蔽某个网站

```shell
iptables -A OUTPUT -m string --string "xx.com" --algo bm --to 65535 -j DROP
service iptables save

#删除屏蔽规则，上面添加的代码是什么样，那么删除的代码就是把-I改成-D 
iptables -D OUTPUT -m string --string "xx.com" --algo bm --to 65535 -j DROP

-A
#添加iptables规则；
-D
#删除iptables规则（把添加防火墙规则时代码中的-A改成-D即可删除添加的规则）；
-m string
#指定模块；
--string "xx.com"
#指定要匹配的字符串(域名、关键词等)；
--algo bm
#指定匹配字符串模式/算法（还有一种更复杂的算法：kmp）；
--to 65535
#指定端口，这里代表所有端口（1-65535）；
-j DROP
#指匹配到数据包后处理方式，这里是丢弃数据包。

```





## Windows免密码登录Linux

1. 先在客户端生成密钥并上传公钥到linux上

```shell
# 打开命令行
ssh-keygen -t rsa
cd .ssh

# 通过scp上传，注意，如果改了ssh的端口，这里要加 -P 参数
scp id_rsa.pub  root@linux:~/
```

2. 将公钥添加到authorized_keys文件中

```shell
# 查看ssh配置是否符合要求
vim /etc/ssh/sshd_cofig

# 取消注释：
RSAAuthentication yes
PubkeyAuthentication yes
AuthorizedKeysFile    .ssh/authorized_keys

# 添加
cat id_rsa.pub >> .ssh/authorized_keys
chmod 600 .ssh/authorized_keys

systemctl restart sshd
```





## ssh反向代理

* 需求

  > A: 内网主机
  >
  > B: 公网服务器
  >
  > C: 自己的电脑

* 步骤

1. 在A上发起反向代理请求

```shell
ssh -fCNR B_ip:B_port:localhost:22 B_user@B_ip -p B_ssh_port
例如：
ssh -fCNR 64.64.239.22:2000:localhost:22 root@64.64.239.22 -p 22

B_port为B的监听端口，可任意设置,注意避免与其他端口冲突
如果B_ssh_port为22 则可省略
-N：不执行任何指令
-f：背景执行
-R：主要建立reverse tunnel的参数

```

这一步的结果是：将A的ssh端口映射到B的监听端口，在B上直接ssh登录这个端口即可。

2. 在C上的操作

* 先登录B

* 在B上进行如下操作

  ```shell
  ssh -p B_port  A_user@127.0.0.1
  
  端口为监听端口
  注意这里的用户是A上的
  ```

  这样就能登录A了。



## Git基本用法

### 1.安装
安装完成后，打开命令行，输入：

```sh
git config --global user.name "Your Name"
git config --global user.email "email@example.com"
```

### 2.添加远程仓库
```sh
git remote add origin git@github.com:Hello/Hello.git
```


### 3.无密码提交
条件：
> 1.使用 SSH 方式来代替 HTTPS 方式
> 
> 2.上传公钥到GitHub

```sh
# 生成公钥
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
# 上传省略
```

```sh
$git remote -v
origin  https://github.com/USERNAME/REPOSITORY.git (fetch)
origin  https://github.com/USERNAME/REPOSITORY.git (push)

#修改
git remote set-url origin git@github.com:USERNAME/REPOSITORY.git

## 验证
$git remote -v
origin  git@github.com:USERNAME/REPOSITORY.git (fetch)
origin  git@github.com:USERNAME/REPOSITORY.git (push)
```

### 4.设置代理
```sh
git config --global http.proxy http://127.0.0.1:1080
git config --global https.proxy https://127.0.0.1:1080
git config --global --unset http.proxy
git config --global --unset https.proxy
#只对github.com
git config --global http.https://github.com.proxy socks5://127.0.0.1:1080
```

由于我使用的是socks代理，也记录一下

```sh
git config --global http.proxy socks5://127.0.0.1:1080
git config --global https.proxy socks5://127.0.0.1:1080
```

好像设置了https代理后出错，那就取消https的代理，留下http的。

### 5.查看git配置

```sh
#查看系统config
git config --system --list

#查看当前用户（global）配置
git config --global  --list

#查看当前仓库配置信息
git config --local  --list
```





## 配置Java环境

jdk下载链接 ： https://www.oracle.com/technetwork/java/javase/downloads/java-archive-javase8u211-later-5573849.html

```sh
tar -zxvf jdk-8u121-linxu-x64.tar.gz 

sudo gedit /etc/profile
#set java environment 
export JAVA_HOME=/opt/java/jdk1.8.0_65
export JRE_HOME=${JAVA_HOME}/jre 
export CLASSPATH=.:$JAVA_HOME/lib:$JRE_HOME/lib:$CLASSPATH 
export PATH=${JAVA_HOME}/bin:${JRE_HOME}/bin:$PATH  

source profile

```



## 查看md5

* Windows

  ```sh
  查看MD5值：
  
  certutil -hashfile 文件名  MD5
  
  查看 SHA1
  
  certutil -hashfile 文件名  SHA1 
  
  查看SHA256
  
  certutil -hashfile 文件名  SHA256
  
  ```

* Linux

  ```sh
  md5sum 文件名
  ```

  

  