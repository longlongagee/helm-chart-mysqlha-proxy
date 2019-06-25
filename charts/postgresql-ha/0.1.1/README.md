## PostgreSQL HA cluster (Stolon)

- 基于Stolon提供高可用(kubernetes 集成)的postgreSQL集群
![asd](https://www.kubernetes.org.cn/img/2017/03/20170312110257.jpg)


> Stolon is a cloud native PostgreSQL manager for PostgreSQL high availability.

- 已经被纳入到官方[Chart仓库](https://github.com/helm/charts/tree/master/stable/stolon)
- 进行Rancher local-chart可配置化、优化调整、镜像打包



## Requirements
* Kubernetes >1.5
* PV support on the underlying infrastructure
* Helm 2.2.0 (for `conditions and flags` support)


## Configuration

The following tables lists the configurable parameters of the helm chart and their default values.

| Parameter                               | Description                                    | Default                                                      |
| --------------------------------------- | ---------------------------------------------- | ------------------------------------------------------------ |
| `image`                                 | `stolon` image repository                      | `sorintlab/stolon`                                           |
| `imageTag`                              | `stolon` image tag                             | `v0.7.0-pg9.6`                                               |
| `imagePullPolicy`                       | Image pull policy                              | `Always` if `imageTag` is `latest`, else `IfNotPresent`      |
| `clusterName`                           | Name of the cluster                            | `kube-stolon`                                                |
| `debug`                                 | Debug mode                                     | `false`                                                      |
| `store.backend`                         | Store backend to use (etcd/consul/kubernetes)  | `etcd`                                                       |
| `store.endpoints`                       | Store backend endpoints                        | `http://etcd-0:2379,http://etcd-1:2379,http://etcd-2:2379`   |
| `store.kubeResourceKind`                | Kubernetes resource kind (only for kubernetes) | `configmap`                                                  |
| `pgReplUsername`                        | Repl username                                  | `repluser`                                                   |
| `pgReplPassword`                        | Repl password                                  | random 40 characters                                         |
| `pgSuperuserName`                       | Postgres Superuser name                        | `stolon`                                                     |
| `pgSuperuserPassword`                   | Postgres Superuser password                    | random 40 characters                                         |
| `sentinel.replicas`                     | Number of sentinel nodes                       | `2`                                                          |
| `sentinel.resources`                    | Sentinel resource requests/limit               | Memory: `256Mi`, CPU: `100m`                                 |
| `sentinel.affinity`                     | Affinity settings for sentinel pod assignment  | `{}`                                                         |
| `sentinel.nodeSelector`                 | Node labels for sentinel pod assignment        | `{}`                                                         |
| `sentinel.tolerations`                  | Toleration labels for sentinel pod assignment  | `[]`                                                         |
| `proxy.replicas`                        | Number of proxy nodes                          | `2`                                                          |
| `proxy.resources`                       | Proxy resource requests/limit                  | Memory: `256Mi`, CPU: `100m`                                 |
| `proxy.affinity`                        | Affinity settings for proxy pod assignment     | `{}`                                                         |
| `proxy.nodeSelector`                    | Node labels for proxy pod assignment           | `{}`                                                         |
| `proxy.tolerations`                     | Toleration labels for proxy pod assignment     | `[]`                                                         |
| `keeper.uid_prefix`                     | Keeper prefix name                             | `keeper`                                                     |
| `keeper.replicas`                       | Number of keeper nodes                         | `2`                                                          |
| `keeper.resources`                      | Keeper resource requests/limit                 | Memory: `256Mi`, CPU: `100m`                                 |
| `keeper.affinity`                       | Affinity settings for keeper pod assignment    | `{}`                                                         |
| `keeper.nodeSelector`                   | Node labels for keeper pod assignment          | `{}`                                                         |
| `keeper.tolerations`                    | Toleration labels for keeper pod assignment    | `[]`                                                         |
| `keeper.client_ssl.enabled`             | Enable ssl encryption                          | `false`                                                      |
| `keeper.client_ssl.certs_secret_name`   | The secret for server.crt and server.key       | `pg-cert-secret`                                             |
| `persistence.enabled`                   | Use a PVC to persist data                      | `false`                                                      |
| `persistence.storageClassName`          | Storage class name of backing PVC              | `standard`                                                   |
| `persistence.accessMode`                | Use volume as ReadOnly or ReadWrite            | `ReadWriteOnce`                                              |
| `persistence.size`                      | Size of data volume                            | `10Gi`                                                       |
| `rbac.create`                           | Specifies if RBAC resources should be created  | `true`                                                       |
| `serviceAccount.create`                 | Specifies if ServiceAccount should be created  | `true`                                                       |
| `serviceAccount.name  `                 | Name of the generated serviceAccount           | Defaults to fullname template                                |

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`.

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example,

