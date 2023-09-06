## 项目简介
&emsp;&emsp;观测云是一款旨在解决云计算，以及云原生时代系统为每一个完整的应用构建全链路的可观测性的云服务平台。  
&emsp;&emsp;本文档主要介绍如何在 Kubernetes 中通过 DaemonSet 方式安装 DataKit。
> 如需使用主机安装（Linux、Windows、MAC），参考 [主机安装介绍](https://docs.guance.com/datakit/datakit-install/)    
> 如需了解更多采集相关材料请参考 [Datakit介绍](https://docs.guance.com/datakit/datakit-arch/)、[Datakit Operator介绍](https://docs.guance.com/datakit/datakit-operator/)

##  [Kubernetes 接入参考](https://docs.guance.com/datakit/datakit-daemonset-deploy/)
通过 yaml 安装 datakit 和 datakit operator
  - 下载yaml文件
```
$ git clone https://github.com/GuanceDemo/guance-java-ruoyi-demo.git
$ cd deployment/datakit
```
  - 更新 datakit.yaml 中的dataway和token 
  >获取方式：登陆观测云空间-->集成--> datakit
```
- name: ENV_DATAWAY
  value: https://openway.guance.com?token=<your-token> # 此处填上 您的DataWay和token信息
```
  - 安装
```
$ kubectl apply -f datakit.yaml
$ kubectl apply -f datakit-operator.yaml
```

  - 验证    
  查看pod是否都运行正常
  ```
  $ kubectl get pod -n datakit
  ```
  登陆观测云空间，查看基础设施里是否有集群信息，若有即为数据上报成功。若无数据，请按照指引进行[无数据排查](https://docs.guance.com/datakit/why-no-data/)。