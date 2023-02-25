# Centos7-install-Python3.9.10

##依赖包安装
###如果是Linux的minimal系统，需要安装：

```
yum install -y vim wget tftp lrzsz bzip2 zip unzip net-tools bind-utils traceroute tcpdump telnet tree mlocate bash-completion rsync readline readline-devel gdisk
```

###编译安装需要的包：
```
yum install -y make.x86_64 gcc gcc-c++ zlib zlib-devel openssl-devel
```
#第一步：下载源码包
前往Python官网下载源码包，例如：3.9.10：https://www.python.org/ftp/python/3.9.10/Python-3.9.10.tgz
```
wget https://www.python.org/ftp/python/3.9.10/Python-3.9.10.tgz #下载源码包
tar -xvf Python-3.9.10.tgz #解压源码包
```
#第二步：编译并安装
```
cd Python-3.9.10 #进入解压出来的文件夹
./configure prefix=/usr/local/python3 --with-ensurepip=install && make -j 4 && make install
#设置安装目录并进行编译后安装
```
#第三步：配置环境变量
```
echo "export PATH=\$PATH:/usr/local/python3/bin" >> /etc/bashrc && source /etc/bashrc 
#更新全局环境
```
#第四步：创建软连接并验证
```
#删除原有的python3软连接
rm -rf /usr/bin/python3 
#创建python3软连接
ln -s /usr/local/python3/bin/python3 /usr/bin/python3 
#验证python3软连接是否正常创建，正常会返回安装的版本信息
python3 -V 
#删除原有的pip3软连接
rm -rf /usr/bin/pip3 
#创建pip3软连接
ln -s /usr/local/python3/bin/pip3 /usr/bin/pip3 
#验证pip3软连接是否正常创建，正常创建会返回pip版本与关联的python版本信息
pip3 -V
```
