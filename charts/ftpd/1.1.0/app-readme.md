# Ftp服务端
Pyftplibd deployment for Rancher

## Details
* 支持多虚拟用户

* 使用被动模式，需要用户指定不被占用的30000-32701端口

* RancherUI支持用户添加，更多用户添加以及修改配置，启动后在：
    - rancher资源 --> 配置映射 --> 找到 `ftpd/user.conf`  添加

    - rancher资源 --> 配置映射 --> 找到 `ftpd/settings.py`  修改
    
    - 重启生效


## Chart Address

Gitlab address  [Rancher-local-chart](http://192.168.6.126/nebula/rancher-local-charts)
using Kubernetes Deployments and Init Containers.  -- ITO department