# helm

### &#x20;helm基础命令和问题汇总

#### 命令：

```
部署新建：
helm install env-standard-manager-server1 . -n hangzhou-test --debug --dry-run 
部署更新 
helm upgrade ipes-test-communication . --set ingress.hosts[0].host=ipes-test -n ipes-test
```

#### 基本流程

```
//先调试chart文件
helm install coordinated-control-server . -n bmp-dev --debug --dry-run
//如果没问题则部署
helm install coordinated-control-server . -n bmp-dev
//查看状态
helm list -n bmp-dev
kubectl get pod -n bmp-dev
helm coordinated-control-server . --set ingress.hosts[0].host=hangzhou-test -n hangzhou-test
```

#### 问题

1. Pod 名称带上helm名称如何去除

```
去查看 /templates/_helpers.tpl 里面的逻辑，pod的名称在这里面设置的。通常是因为Values.fullnameOverride没设置，
然后采用了Release.Name导致的（*注：不行再看这里：或者在 Helm 的模板中使用自定义的名称，而不是使用默认的 release 名称作为前缀。例如，在 Chart 的模板文件中，可以使用 .Release.Name 获取 release 名称，你可以将其替换为空字符串或者其他自定义的值。例如，将以下模板中的 .Release.Name 替换为 ""，即可去除 Helm 安装名称前缀。）
​
​
SAP：供应链可视化
SAP 销售订单接口：
测试数据：
https://esbtest.fpi-inc.com:8085/sap/function
正式数据：
https://esb.fpi-inc.com:8085/sap/function
​
```

\
