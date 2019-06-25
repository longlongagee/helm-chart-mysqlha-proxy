# Ftp服务端
Pyftplibd deployment for Rancher

## Details
* 支持多虚拟用户

* 使用被动模式，需要用户指定不被占用的30000-32701端口

* RancherUI支持用户添加，更多用户添加以及修改配置，启动后在：
    - rancher资源 --> 配置映射 --> 找到 `ftpd/user.conf`  添加

    - rancher资源 --> 配置映射 --> 找到 `ftpd/settings.py`  添加

    - 重启生效

## Chart Address

Gitlab address  [Rancher-local-chart](http://192.168.6.126/nebula/rancher-local-charts)
using Kubernetes Deployments and Init Containers.  -- ITO department

## Configuration

映射到`/etc/vsftpd/`下

> user.conf 

```bash
vi /etc/vsftpd/user.conf
#用户名   密码      权限      目录
admin     admin  elradfmwM  /xxx/

# 权限说明：
# 读权限 ：
# e     改变文件目录
# l     列出文件
# r     从服务器接收文件
# 写权限 ：
# a     文件上传
# d     删除文件
# f     文件重命名
# m     创建文件
# w     写权限
# M     文件传输模式（通过FTP设置文件权限 ）  
```
> settings.py

```bash
ip = '0.0.0.0'

port = '21'

# 上传速度限制  100MB/s
max_upload = 100 * 1024 * 1024

# 下载速度限制 100MB/s
max_download = 100 * 1024 * 1024

# 最大连接数
max_cons = 150

# 最多IP数
max_per_ip = 10

# 是否开启匿名访问 on|off
enable_anonymous = 'off'

# 匿名用户目录
anonymous_path = '/home/hx'

```