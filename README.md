# guance-datakit-demo
本文档主要介绍如何安装观测云 Demo 使用的 DataKit 和 DataKit Operator。

> 如需了解更多采集相关材料请参考 [Datakit 介绍](https://docs.guance.com/datakit/datakit-arch/)，[Datakit Operator 介绍](https://docs.guance.com/datakit/datakit-operator/)


## 准备物料
- 下载yaml文件
```shell
git clone https://github.com/GuanceDemo/guance-java-ruoyi-demo.git
cd deployment
```

## 安装 metric-server
> 若 Kubernetes 集群已安装 metric-server，可跳过该步骤

```shell
kubectl apply -f components.yaml
```

## 安装 DataKit Operator
```shell
kubectl create ns datakit
kubectl apply -f datakit-operator.yaml
```

##  安装 DataKit
-  更新 datakit.yaml 中的 ENV_DATAWAY
> 获取方式：登陆观测云空间 --> 集成 --> DataKit

```shell
- name: ENV_DATAWAY
  value: https://openway.guance.com?token=<your-token> # 此处填上 您的 DataWay 和 token 信息
```

- 安装
```shell
kubectl apply -f datakit.yaml
```

- 验证：登陆观测云空间，查看基础设施里是否有集群信息，若有即为数据上报成功。若无数据，请按照指引进行 [无数据排查](https://docs.guance.com/datakit/why-no-data/)。
```
kubectl get pod -n datakit
``` 

## 卸载
```shell
kubectl delete -f datakit-operator.yaml
kubectl delete -f datakit.yaml
```