# k8s-kafaka

## Requirements

```
k8s1.12+ cluster 正常运行，nfs服务用于提供持久化存储
```

## kafka-zk version

```
kafka-2.1.0、scala-2.11、zk-3.4.10
```

## Build image

```bash
sh run.sh
```
```
这里run.sh是直接上传到我的dockerhub，可以把地址改成自己的私有仓库地址
```
## Deploymet

```bash
kubectl  create -f zk.yaml
kubectl  create -f kafka.yaml
```
```
默认部署在default这个namesapce里面。
测试zk：
kubectl exec -it zk-0 -- zkServer.sh status
kubectl exec -it zk-0 -- zkCli.sh create /hello world
kubectl delete -f zk.yaml 
kubectl apply -f zk.yaml
kubectl exec -it zk-0 -- zkCli.sh get /hello
```

```
线上使用的时候注意修改资源，如mem、cpu、磁盘空间大小。根据自己的需求进行修改，本次创建的是3节点的集群，如有其他需求，直接scale进行扩容，注意
不要超过nfs提供的空间大小，否则会启动失败，我使用的storageClass动态申请资源。
```

## Statefulset

```
参考：https://kubernetes.io/docs/tutorials/stateful-application/
```
