# Setting up RexRay on Google Cloud Platform for Kubernetes

# Pre-requisite

- A Ubuntu 17.10 instance 

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

```
./kubectl get --all-namespaces pods
NAMESPACE     NAME                                            READY     STATUS    RESTARTS   AGE
kube-system   etcd-server-events-kubernetes-master            1/1       Running   0          9m
kube-system   etcd-server-kubernetes-master                   1/1       Running   0          10m
kube-system   event-exporter-v0.1.7-64464bff45-dkqqm          1/1       Running   0          10m
kube-system   fluentd-gcp-v2.0.10-74gkl                       1/1       Running   0          10m
kube-system   fluentd-gcp-v2.0.10-lrfxk                       1/1       Running   0          10m
kube-system   fluentd-gcp-v2.0.10-pdng4                       1/1       Running   0          10m
kube-system   fluentd-gcp-v2.0.10-tq6jg                       1/1       Running   0          10m
kube-system   heapster-v1.5.0-584689c78d-285ht                4/4       Running   0          8m
kube-system   kube-addon-manager-kubernetes-master            1/1       Running   0          9m
kube-system   kube-apiserver-kubernetes-master                1/1       Running   0          9m
kube-system   kube-controller-manager-kubernetes-master       1/1       Running   0          10m
kube-system   kube-dns-774d5484cc-8l2gm                       3/3       Running   0          10m
kube-system   kube-dns-774d5484cc-gk4c8                       3/3       Running   0          9m
kube-system   kube-dns-autoscaler-69c5cbdcdd-dl4tw            1/1       Running   0          10m
kube-system   kube-proxy-kubernetes-minion-group-39rs         1/1       Running   0          10m
kube-system   kube-proxy-kubernetes-minion-group-3f46         1/1       Running   0          10m
kube-system   kube-proxy-kubernetes-minion-group-3fpc         1/1       Running   0          10m
kube-system   kube-scheduler-kubernetes-master                1/1       Running   0          10m
kube-system   kubernetes-dashboard-775fc9968-nrk4l            1/1       Running   3          10m
kube-system   l7-default-backend-57856c5f55-bthnz             1/1       Running   0          10m
kube-system   l7-lb-controller-v0.9.7-kubernetes-master       1/1       Running   0          9m
kube-system   metrics-server-v0.2.1-7f8dd98c8f-6vfw8          2/2       Running   0          9m
kube-system   monitoring-influxdb-grafana-v4-554f5d97-2n8mv   2/2       Running   0          10m
kube-system   rescheduler-v0.3.1-kubernetes-master            1/1       Running   0          9m
```

## Installing RexRay Volume Plugin

```
docker plugin install --grant-all-permissions rexray/gcepd GCEPD_TAG=rexray


latest: Pulling from rexray/gcepd
9d3ade925ffa: Download complete 
Digest: sha256:191be8b0fa8f9ab781b61593047310d17f847dc8b8361d4d4731149ecc3ea10d
Status: Downloaded newer image for rexray/gcepd:latest
Installed plugin rexray/gcepd
```

## Listing the Volume Plugins

```
docker plugin ls
ID                  NAME                  DESCRIPTION                        ENABLED
f6796ddcd771        rexray/gcepd:latest   REX-Ray for GCE Persistent Disks   true
```

## Creating the Storage Volume

```
$ docker volume create --driver rexray/gcepd --name storage1 -o 32
storage1
```
## Listing the Volume 
```
$ docker volume ls
DRIVER                VOLUME NAME
rexray/gcepd:latest   storage1
```

## Inspecting the RexRay Volume
```
$ docker volume inspect storage1
[
    {
        "Driver": "rexray/gcepd:latest",
        "Labels": {},
        "Mountpoint": "/var/lib/docker/plugins/f6796ddcd7711b7ad931a2a4235441adb4454d434b7314400099146876a395d0/rootfs",
        "Name": "storage1",
        "Options": {
            "32": ""
        },
        "Scope": "global",
        "Status": {
            "availabilityZone": "us-central1-b",
            "fields": null,
            "iops": 0,
            "name": "storage1",
            "server": "gcepd",
            "service": "gcepd",
            "size": 16,
            "type": "pd-ssd"
        }
    }
]

```

## Verifying the Disk under Google Cloud Platform

```
 storage1
Type
SSD persistent disk
Size
16 GB
Zone
us-central1-b
Estimated performance
Operation Type	Read	Write
Sustained random IOPS limit	480.00	480.00
Sustained throughput limit (MB/s)	7.68	7.68
Encryption
Automatic
Equivalent REST
```

