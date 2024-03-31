

# EaseMesh 命令行

- [EaseMesh 命令行：](#easemesh-command-line)
  - [emctl install](#emctl-install)
  - [emctl reset](#emctl-reset)
  - [emctl apply](#emctl-apply)
  - [emctl get](#emctl-get)
  - [emctl delete](#emctl-delete)
  - [速查表](#速查表)

`emctl` 是处理 EaseMesh 资源的专用命令，它运行在 [Easegress](https://github.com/megaease/easegress) MeshController 中，在不同的实例中具有不同的角色。 `MeshController` 会在 `Easegress` 中注册自己的管理 API，因此 `emctl` 中的服务器标志与 Easegress 的相同。


运行 `emctl --help` 或 `emctl help <subcommand>` 可以获取每个子命令的细节。

## emctl install

部署 EaseMesh 的基础设施组件。

```bash
emctl install [标志]

# Examples
emctl install --mesh-namespace mesh-demo --clean-when-failed
```

| 标志                                              | 简写  | 描述                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ----------------------------------------------- | --- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| --add-ons                                       |     | 要安装的附加组件的名称                                                                                                                                                                                                                                                                                                                                                                                                                              |
| --clean-when-failed                             |     | 安装失败时清理资源 (默认: true)                                                                                                                                                                                                                                                                                                                                                                                                                     |
| --easegress-image string                        |     | Easegress 镜像名 (默认: "megaease/easegress:easemesh")                                                                                                                                                                                                                                                                                                                                                                                        |
| --easemesh-control-plane-replicas int           |     | 网格控制平面副本数 (默认: 3)                                                                                                                                                                                                                                                                                                                                                                                                                        |
| --easemesh-ingress-replicas int                 |     | 网格入口控制器副本数 (默认: 1)                                                                                                                                                                                                                                                                                                                                                                                                                       |
| --easemesh-operator-image string                |     | 网格控制器镜像名 (默认: "megaease/easemesh-operator:latest")                                                                                                                                                                                                                                                                                                                                                                                       |
| --easemesh-operator-replicas int                |     | 网格 operator 控制器副本数 (默认: 1)                                                                                                                                                                                                                                                                                                                                                                                                               |
| --file string                                   | -f  | 指定安装参数的 yaml 文件                                                                                                                                                                                                                                                                                                                                                                                                                          |
| --heartbeat-interval int                        |     | 网格服务的心跳间隔 (默认: 5)                                                                                                                                                                                                                                                                                                                                                                                                                        |
| --help                                          | -h  | 帮助                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| --image-registry-url string                     |     | 镜像注册 URL (默认: "docker.io")                                                                                                                                                                                                                                                                                                                                                                                                               |
| --mesh-control-plane-admin-port int             |     | 用于管理的网格控制平面管理端口 (默认: 2381)                                                                                                                                                                                                                                                                                                                                                                                                               |
| --mesh-control-plane-check-healthz-max-time int |     | 检查控制面板组件是否准备就绪的最大超时时间 (秒，默认: 60)                                                                                                                                                                                                                                                                                                                                                                                                         |
| --mesh-control-plane-client-port int            |     | 网格控制平面用于远程访问的客户端端口 (默认: 2379)                                                                                                                                                                                                                                                                                                                                                                                                            |
| --mesh-control-plane-peer-port int              |     | 网格控制平面的端口，用于达成共识 (默认: 2380)                                                                                                                                                                                                                                                                                                                                                                                                              |
| --mesh-control-plane-pv-capacity string         |     | EaseMesh 控制平面需要 PersistentVolume 来存储数据。你需要预先创建 PersistentVolume 并指定其 storageClassName 作为 --mesh-storage-class-name 的值。您可以通过以下定义创建 PersistentVolume:  apiVersion: v1 kind: PersistentVolume metadata:   labels:     app: easemesh   name: easemesh-pv spec:   storageClassName: {easemesh-storage}   accessModes:   - {ReadWriteOnce}   capacity:     storage: {3Gi}   hostPath:     path: {/opt/easemesh/}     type: "DirectoryOrCreate" |
| --mesh-control-plane-service-admin-port int     |     | Easegress 管理地址端口 (默认: 2381)                                                                                                                                                                                                                                                                                                                                                                                                              |
| --mesh-control-plane-service-name string        |     | 网格控制平面服务名 (默认: "easemesh-control-plane-service")                                                                                                                                                                                                                                                                                                                                                                                         |
| --mesh-control-plane-service-peer-port int      |     | Easegress 集群对端端口 (默认: 2380)                                                                                                                                                                                                                                                                                                                                                                                                              |
| --mesh-ingress-service-port int32               |     | 网格入口控制器端口 (默认: 19527)                                                                                                                                                                                                                                                                                                                                                                                                                    |
| --mesh-namespace string                         |     | EaseMesh 在 k8s 的命名空间 (默认: "easemesh")                                                                                                                                                                                                                                                                                                                                                                                                    |
| --mesh-storage-class-name string                |     | 网格存储类的类名 (默认: "easemesh-storage")                                                                                                                                                                                                                                                                                                                                                                                                        |
| --registry-type string                          |     | 应用服务注册的注册类型，支持 eureka、consul、nacos (默认: "eureka")                                                                                                                                                                                                                                                                                                                                                                                        |
| --only-add-on                                   |     | 只安装附加组件 (默认为 false, 当设为 true, 必须通过 `--add-ons` 指定至少一个附加组件)                                                                                                                                                                                                                                                                                                                                                                               |

## emctl reset

重置 EaseMesh 的基础设施组件

```bash
emctl reset [标志]

# Examples
emctl reset --mesh-namespace mesh-demo
```

| 标志                                       | 简写  | 描述                                                         |
| ---------------------------------------- | --- | ---------------------------------------------------------- |
| --add-ons                                |     | 需要卸载的附加组件名                                                 |
| --help                                   | -h  | 帮助                                                         |
| --mesh-control-plane-service-name string |     | 网格控制平面服务名 (默认: "easemesh-control-plane-service")           |
| --mesh-namespace string                  |     | EaseMesh 在 kubernetes 的命名空间 (默认: "easemesh")               |
| --only-add-on                            |     | 只卸载附加组件 (默认为 false, 当设为 true, 必须通过 `--add-ons` 指定至少一个附加组件) |

## emctl apply

应用一个配置到 Easemesh.

```bash
emctl apply [标志]

# Examples
emctl apply -f config.yaml
```

| 标志                 | 简写  | 描述                                             |
| ------------------ | --- | ---------------------------------------------- |
| --file string      | -f  | 包含要应用的 EaseMesh 资源文件（YAML 格式）的位置，可以是文件、目录或 URL |
| --help             | -h  | 帮助                                             |
| --recursive        | -r  | 是否递归迭代该位置的所有子目录和文件 (默认: true)                  |
| --server string    | -s  | 访问 EaseMesh 控制平面的地址 (默认: "127.0.0.1:2381")     |
| --timeout duration | -t  | 限制请求 EaseMesh 控制平面的最大超时的持续时间 (默认: 30s)         |

## emctl get

获取 Easemesh 的资源文件

```bash
emctl get [标志]

# Examples
emctl get -f config.yaml
emctl get service service-001
```

| 标志                 | 简写  | 描述                                         |
| ------------------ | --- | ------------------------------------------ |
| --help             | -h  | 抱住                                         |
| --output string    | -o  | 输出格式 (支持 table, yaml, json) (默认: "table")  |
| --server string    | -r  | 访问 EaseMesh 控制平面的地址 (默认: "127.0.0.1:2381") |
| --timeout duration | -t  | 限制请求 EaseMesh 控制平面的最大超时的持续时间 (默认: 30s)     |

## emctl delete

删除 Easemesh 的资源文件

```bash
emctl delete [标志]

# Examples
emctl delete -f config.yaml
emctl delete service service-001
```

| 标志                 | 简写  | 描述                                             |
| ------------------ | --- | ---------------------------------------------- |
| --file string      | -f  | 包含要删除的 EaseMesh 资源文件（YAML 格式）的位置，可以是文件、目录或 URL |
| --help             | -h  | 帮助                                             |
| --recursive        | -r  | 是否递归遍历该位置的所有子目录和文件 (默认: true)                  |
| --server string    | -s  | 访问 EaseMesh 控制平面的地址 (默认: "127.0.0.1:2381")     |
| --timeout duration | -t  | 限制请求 EaseMesh 控制平面的最大超时的持续时间 (default 30s)     |

## 速查表

```bash
# 安装 EaseMesh 组件
emctl install --clean-when-failed

# 注册租户
echo 'apiVersion: mesh.megaease.com/v1alpha1
kind: Tenant
metadata:
  name: tenant-001
  labels: {}
services: []
description: tenant-001' | emctl apply -f -

# 注册租户
emctl apply -f tenant-001.yaml

# 注册服务
emctl apply -f service-001.yaml

# 注册服务
echo 'kind: Service
metadata:
  name: service-001
spec:
  registerTenant: "tenant-001"
  sidecar: {}' | emctl apply -f -

# 注册负载均衡
echo 'apiVersion: mesh.megaease.com/v1alpha1
kind: LoadBalance
metadata:
  name: service-001
spec:
  policy: random' | emctl apply -f -

# 注册入口
echo 'apiVersion: mesh.megaease.com/v1alpha1
kind: Ingress
metadata:
  name: service-001
  labels: {}
spec:
  rules:
  - paths:
    - path: .*
      backend: service-001' | emctl apply -f -

# 获取租户 (kind 在命令行中不区分大小写)
emctl get tenant -o yaml

# 获取服务
emctl get service
emctl get service -o yaml
emctl get service service-001 -o json

# 获取负载均衡
emctl get loadbalance
emctl get loadbalance service-001 -o yaml

# 删除服务
emctl delete service service-001
emctl delete service -f service-001.yaml

# 删除负载均衡
emctl delete loadbalance service-001

# NOTE: 以下Service附带种类的操作与负载均衡相同:
# - Sidecar
# - Resilience
# - Canary
# - ObservabilityMetrics, ObservabilityTracings, ObservabilityOutputServer
```
