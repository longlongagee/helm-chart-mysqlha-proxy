## MySQL HA Cluster + MySQL-Proxy deployment for rancher

### 通过

```bash
# 指定密码、nodePort、server—name等等
helm install -set "slave.rootPassWord=xxx,master.rootPassWord=xxx" local/mysqlha --name mytest
# 具体配置参数查看：
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
