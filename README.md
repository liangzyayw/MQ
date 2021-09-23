## MQ
消息队列等服务；如: zookeeper、Kafka等

## Dockerfile
`zookeeper`

```
zookeeper-Dockerfile

## 命名空间
`执行mq-namespace.yaml文件`
```
kubectl create -f mq-namespace.yaml
```
## zookeeper
`Dockerfile`
>在zookeeper-Dockerfile目录执行下列操作
```
## 下载资源包
wget https://wget.52liangzy.top/MQ/jdk.tar.gz
wget https://wget.52liangzy.top/MQ/zookeeper.tar.gz

## 将zookeeper打包成镜像
docker build -t zookeeper:3.5.9 .

## 检查镜像包
[root@k8s-master ~]# docker images | grep zookeeper
zookeeper      3.5.9        49c6b6204e9d   5 days ago      602MB
```

`执行一下yaml文件`
```
## 对外暴露端口
kubectl create -f  zookeeper-service.yaml

## pvc持久化存储卷
kubectl create -f  zookeeper-pvc-data.yaml
kubectl create -f  zookeeper-pvc-logs.yaml

## deployment服务部署
kubectl create -f  zookeeper-deployment.yaml
```

## kafka
`Dockerfile`
>在kafka-Dockerfile目录执行下列操作
```
## 下载资源包
wget https://wget.52liangzy.top/MQ/jdk.tar.gz
wget https://wget.52liangzy.top/MQ/kafka.tar.gz

## 将zookeeper打包成镜像
docker build -t kafka:2.13-2.8.0 .

## 检查镜像包
[root@k8s-master mysql]# docker images | grep kafka
kafka          2.13-2.8.0   d85456009233   4 days ago      649MB
```

`执行一下yaml文件`
```
## 对外暴露端口
kubectl create -f  kafka-service.yaml

## pvc持久化存储卷
kubectl create -f  kafka-pvc-logs.yaml

## deployment服务部署
kubectl create -f  kafka-deployment.yaml
```

## 查看执行结果
`查看pod`
``
>[root@k8s-master ~]# kubectl get pod -n mq
```
NAME                        READY   STATUS    RESTARTS   AGE
kafka-849c85f6bc-cn75n      1/1     Running   0          4d23h
zookeeper-d48d45dbf-b5ktn   1/1     Running   0          5d2h
```
`查看pvc`
>[root@k8s-master ~]# kubectl get pvc -n mq
```
NAME             STATUS   VOLUME           CAPACITY   ACCESS MODES   STORAGECLASS   AGE
kafka-logs       Bound    kafka-logs       10Gi       RWO                           4d23h
zookeeper-data   Bound    zookeeper-data   10Gi       RWO                           5d3h
zookeeper-logs   Bound    zookeeper-logs   10Gi       RWO                           5d3h
```
`查看service`
>[root@k8s-master ~]# kubectl get service -n mq
```
NAME        TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)    AGE
kafka       ClusterIP   10.103.131.97   <none>        9092/TCP   4d23h
zookeeper   ClusterIP   10.102.94.110   <none>        2181/TCP   5d3h
```
