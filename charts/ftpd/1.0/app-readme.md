# Ftp服务端
pyftplibd deployment for Rancher


## Details
* 支持多虚拟用户
  - RancherUI支持用户添加，更多用户容器启动后，进入容器添加：
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
  - 重启后生效
  
* 使用被动模式，需要用户指定不被占用的30000-32701端口

## Chart Address

Gitlab address  [Rancher-local-chart](http://192.168.6.126/nebula/rancher-local-charts)
using Kubernetes Deployments and Init Containers.  -- ITO department
