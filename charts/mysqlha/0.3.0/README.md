## MySQL HA Cluster + MySQL-Proxy deployment for rancher


_v0.3.0_

### 通过Rancher商店进行部署:
#### 可选参数


| 可选参数                            |      描述                         |  默认值                                              |
| ---------------------------------- | -------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------- |
| `master.name`                                 | 主库服务名                                    |                      `master` |
| `master.rootPassWord`              | 主库的root密码                                                                                                                | `hantele123`                                     |
| `master.replUser` | 主库的同步的帐号 | `repl` |
| `master.replPassword` | 主库同步的帐号密码 | `repl@2019` |
| `slave.name` | 备库服务名 | `slave` |
| `slave.rootPassWord` | 主库的root密码 | `hantele123` |
| `slave.replUser` | 备库的同步的帐号 | `repl` |
| `slave.replPassword` | 备库同步的帐号密码 | `repl@2019` |
| `proxy.type` | 代理服务外部访问类型 | `NodePort` |
| `proxy.name` | 代理服务名 | `proxy` |
| `proxy.image` | 代理使用镜像 | `192.168.6.96:8098/mysql-proxy` |
| `proxy.tag` | 代理镜像tag | `2.0` |



### 通过helm 进行安装：


```bash
# 指定密码、nodePort、server—name等等
helm install -set "slave.rootPassWord=xxx,master.rootPassWord=xxx" local/mysqlha --name mytest

```
#### 具体配置参数查看命令
```bash
helm inspect values local/mysqlha
-> apiVersion: v1
appVersion: "1.0"
description: MySQL HA Cluster + MySQL-Proxy deployment for rancher
name: mysqlha
version: 0.1.2

---
# Default values for mysqlha.
# This is a YAML-formatted file.
# Declare variables to be passed into your templates.

replicaCount: 1

image:
  repository: mysql
  tag: "5.7.24"
  pullPolicy: IfNotPresent

nameOverride: ""
fullnameOverride: ""

persistence:
  enabled: true
  ## database data Persistent Volume Storage Class
...
...

```
