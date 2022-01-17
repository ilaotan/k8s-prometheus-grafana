# k8s-prometheus-grafana

[Kubernetes+Prometheus+Grafana部署笔记](http://blog.51cto.com/blogger/publish/2160569)  

[Kubernetes+Prometheus+Grafana部署笔记](https://www.cnblogs.com/yangxiaochu/p/10838570.html)  


[apisix安装prometheus-grafana](https://apisix.apache.org/blog/2021/12/13/monitor-apisix-ingress-controller-with-prometheus)


[官方文档 k8s安装grafana](https://grafana.com/docs/grafana/latest/installation/kubernetes/)

`

#安装git，下载yaml
git clone https://github.com/redhatxl/k8s-prometheus-grafana.git
git clone https://github.com/ilaotan/k8s-prometheus-grafana.git
#安装node-exporter
kubectl create -f  node-exporter.yaml 
#安装prometheus组件
kubectl create -f  prometheus/rbac-setup.yaml
kubectl create -f  prometheus/configmap.yaml 
kubectl create -f  prometheus/prometheus.deploy.yml 
kubectl create -f  prometheus/prometheus.svc.yml 
#安装 grafana 组件
kubectl create -f  grafana/grafana-deploy.yaml
kubectl create -f  grafana/grafana-svc.yaml
kubectl create -f  grafana/grafana-ing.yaml

# 官方版本 仅修改了namespace
kubectl create -f  grafana_new/all.yaml


# 移除

#node-exporter
kubectl delete -f  node-exporter.yaml 
#prometheus组件
kubectl delete -f  prometheus/rbac-setup.yaml
kubectl delete -f  prometheus/configmap.yaml 
kubectl delete -f  prometheus/prometheus.deploy.yml 
kubectl delete -f  prometheus/prometheus.svc.yml 
#grafana 组件
kubectl delete -f  grafana/grafana-deploy.yaml
kubectl delete -f  grafana/grafana-svc.yaml
kubectl delete -f  grafana/grafana-ing.yaml



查看组件服务的映射端口

kubectl get svc -n kube-system


访问
1、prometheus http://ip:30003  2、grafana http://ip:31112 （默认用户密码 admin admin）
3、配置grafana 数据源为prometheus


update:  修改为
  type: ClusterIP
  externalIPs:
    - 172.16.100.52



导入dashboard面板
Grafana.net Dashboard 315

`

apisix开启grafana
查到两个文档  其中第一个有点生涩, 使用了自定义Kind  改不动
https://apisix.apache.org/blog/2021/12/13/monitor-apisix-ingress-controller-with-prometheus/  
https://apisix.apache.org/docs/ingress-controller/plugins/prometheus/#enable-prometheus



