# Setting up RexRay on Google Cloud Platform for Kubernetes

# Pre-requisite

- 1 Master & 2 Worker Node Instance

# Installing Kubernetes

```
babacoders@manager1:~$ sudo curl -sS https://get.k8s.io | bash
```


```

$ kubernetes/cluster/kube-up.sh 

..
Cluster validation succeeded
Done, listing cluster services:
Kubernetes master is running at https://104.198.234.137
GLBCDefaultBackend is running at https://104.198.234.137/api/v1/namespaces/kube-system/services/default-http-backend:http/proxy
Heapster is running at https://104.198.234.137/api/v1/namespaces/kube-system/services/heapster/proxy
KubeDNS is running at https://104.198.234.137/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
kubernetes-dashboard is running at https://104.198.234.137/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy
Metrics-server is running at https://104.198.234.137/api/v1/namespaces/kube-system/services/https:metrics-server:/proxy
Grafana is running at https://104.198.234.137/api/v1/namespaces/kube-system/services/monitoring-grafana/proxy
InfluxDB is running at https://104.198.234.137/api/v1/namespaces/kube-system/services/monitoring-influxdb:http/proxy
To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.

```

# Using Kubectl 

```
@manager1:~/kubernetes/client$ ./bin/kubectl get nodes
NAME                           STATUS                     ROLES     AGE       VERSION
kubernetes-master              Ready,SchedulingDisabled   <none>    4m        v1.9.3
kubernetes-minion-group-39rs   Ready                      <none>    3m        v1.9.3
kubernetes-minion-group-3f46   Ready                      <none>    3m        v1.9.3
kubernetes-minion-group-3fpc   Ready                      <none>    3m        v1.9.3
```

#

```
/kubectl get --all-namespaces services
NAMESPACE     NAME                   TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)             AGE
default       kubernetes             ClusterIP   10.0.0.1       <none>        443/TCP             6m
kube-system   default-http-backend   NodePort    10.0.68.176    <none>        80:30147/TCP        6m
kube-system   heapster               ClusterIP   10.0.82.84     <none>        80/TCP              6m
kube-system   kube-dns               ClusterIP   10.0.0.10      <none>        53/UDP,53/TCP       6m
kube-system   kubernetes-dashboard   ClusterIP   10.0.10.53     <none>        443/TCP             6m
kube-system   metrics-server         ClusterIP   10.0.124.11    <none>        443/TCP             6m
kube-system   monitoring-grafana     ClusterIP   10.0.225.128   <none>        80/TCP              6m
kube-system   monitoring-influxdb    ClusterIP   10.0.41.250    <none>        8083/TCP,8086/TCP   6m
```
