# Setting up RexRay on Google Cloud Platform for Kubernetes

# Pre-requisite

- 1 Master & 2 Worker Node Instance

# Installing Kubernetes

```


babacoders@manager1:~$ sudo curl -sS https://get.k8s.io | bash
'kubernetes' directory already exist. Should we skip download step and start to create cluster based on it? [Y]/n
Skipping download step.
Creating a kubernetes on gce...
... Starting cluster in us-central1-b using provider gce
... calling verify-prereqs
... calling verify-kube-binaries
... calling kube-up
Project: spheric-temple-187614
Network Project: spheric-temple-187614
Zone: us-central1-b
BucketNotFoundException: 404 gs://kubernetes-staging-99eb322adf bucket does not exist.
Creating gs://kubernetes-staging-99eb322adf
Creating gs://kubernetes-staging-99eb322adf/...
+++ Staging server tars to Google Storage: gs://kubernetes-staging-99eb322adf/kubernetes-devel
+++ kubernetes-server-linux-amd64.tar.gz uploaded (sha1 = a78baf716436e81ec23655009287a7e42116ec03)
+++ kubernetes-salt.tar.gz uploaded (sha1 = 88451d9460f86568bb4410421d677b8fd1adc11d)
+++ kubernetes-manifests.tar.gz uploaded (sha1 = d5f8a8344223d141daead7248f58139f17da6826)
INSTANCE_GROUPS=
NODE_NAMES=
Looking for already existing resources
Found existing network default in AUTO mode.
Creating firewall...
.Creating firewall...
IP aliases are disabled.
..Creating firewall...
..Found subnet for region us-central1 in network default: default
Starting master and configuring firewalls
...Creating firewall...
.................Created [https://www.googleapis.com/compute/v1/projects/spheric-temple-187614/zones/us-central1-b/disks/kubernetes-master-pd].
.NAME                  ZONE           SIZE_GB  TYPE    STATUS
kubernetes-master-pd  us-central1-b  20       pd-ssd  READY
New disks are unformatted. You must format and mount a disk before it
can be used. You can find instructions on how to do this at:
https://cloud.google.com/compute/docs/disks/add-persistent-disk#formatting
........Creating firewall...
..Created [https://www.googleapis.com/compute/v1/projects/spheric-temple-187614/global/firewalls/kubernetes-default-internal-master].
.done.
NAME 
.........Created [https://www.googleapis.com/compute/v1/projects/spheric-temple-187614/global/firewalls/default-default-ssh].
..done.
NAME                 NETWORK  DIRECTION  PRIORITY  ALLOW   DENY
default-default-ssh  default  INGRESS    1000      tcp:22
.Created [https://www.googleapis.com/compute/v1/projects/spheric-temple-187614/regions/us-central1/addresses/kubernetes-master-ip].
..Created [https://www.googleapis.com/compute/v1/projects/spheric-temple-187614/global/firewalls/kubernetes-master-https].
done.
..NAME                     NETWORK  DIRECTION  PRIORITY  ALLOW    DENY
kubernetes-master-https  default  INGRESS    1000      tcp:443
..Generating certs for alternate-names: IP:35.188.206.177,IP:10.0.0.1,DNS:kubernetes,DNS:kubernetes.default,DNS:kubernetes.default.svc,DNS:kubernetes
.default.svc.cluster.local,DNS:kubernetes-master
Created [https://www.googleapis.com/compute/v1/projects/spheric-temple-187614/global/firewalls/kubernetes-default-internal-node].
.done.
NAME                              NETWORK  DIRECTION  PRIORITY  ALLOW                         DENY
kubernetes-default-internal-node  default  INGRESS    1000      tcp:1-65535,udp:1-65535,icmp
....Created [https://www.googleapis.com/compute/v1/projects/spheric-temple-187614/global/firewalls/kubernetes-master-etcd].
done.
NAME                    NETWORK  DIRECTION  PRIORITY  ALLOW              DENY
kubernetes-master-etcd  default  INGRESS    1000      tcp:2380,tcp:2381
Unable to successfully run 'cfssl' from /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin; downloadi
ng instead...
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  9.8M  100  9.8M    0     0  3377k      0  0:00:03  0:00:03 --:--:-- 2715k
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 2224k  100 2224k    0     0  1112k      0  0:00:02  0:00:02 --:--:-- 1017k
2018/02/14 17:27:36 [INFO] generating a new CA key and certificate from CSR
2018/02/14 17:27:36 [INFO] generate received request
2018/02/14 17:27:36 [INFO] received CSR
2018/02/14 17:27:36 [INFO] generating key: ecdsa-256
2018/02/14 17:27:36 [INFO] encoded CSR
2018/02/14 17:27:36 [INFO] signed certificate with serial number 135845880321732853208489813166927296022999926575
Generate peer certificates...
2018/02/14 17:27:36 [INFO] generate received request
2018/02/14 17:27:36 [INFO] received CSR
2018/02/14 17:27:36 [INFO] generating key: ecdsa-256
2018/02/14 17:27:36 [INFO] encoded CSR
2018/02/14 17:27:36 [INFO] signed certificate with serial number 698273047460038177268714481224204499306248381340
+++ Logging using Fluentd to gcp
Creating firewall...
...........Created [https://www.googleapis.com/compute/v1/projects/spheric-temple-187614/global/firewalls/kubernetes-minion-all].
done.
NAME                   NETWORK  DIRECTION  PRIORITY  ALLOW                     DENY
kubernetes-minion-all  default  INGRESS    1000      tcp,udp,icmp,esp,ah,sctp
WARNING: You have selected a disk size of under [200GB]. This may result in poor I/O performance. For more information, see: https://developers.googl
e.com/compute/docs/disks#performance.
Created [https://www.googleapis.com/compute/v1/projects/spheric-temple-187614/zones/us-central1-b/instances/kubernetes-master].
NAME               ZONE           MACHINE_TYPE   PREEMPTIBLE  INTERNAL_IP  EXTERNAL_IP     STATUS
kubernetes-master  us-central1-b  n1-standard-1               10.128.0.2   35.188.206.177  RUNNING
Creating nodes.
Using subnet default
Attempt 1 to create kubernetes-minion-template
WARNING: You have selected a disk size of under [200GB]. This may result in poor I/O performance. For more information, see: https://developers.googl
e.com/compute/docs/disks#performance.
Created [https://www.googleapis.com/compute/v1/projects/spheric-temple-187614/global/instanceTemplates/kubernetes-minion-template].
NAME                        MACHINE_TYPE   PREEMPTIBLE  CREATION_TIMESTAMP
kubernetes-minion-template  n1-standard-2               2018-02-14T09:27:59.126-08:00
Created [https://www.googleapis.com/compute/v1/projects/spheric-temple-187614/zones/us-central1-b/instanceGroupManagers/kubernetes-minion-group].
NAME                     LOCATION       SCOPE  BASE_INSTANCE_NAME       SIZE  TARGET_SIZE  INSTANCE_TEMPLATE           AUTOSCALED
kubernetes-minion-group  us-central1-b  zone   kubernetes-minion-group  0     3            kubernetes-minion-template  no
Waiting for group to become stable, current operations: creating: 3
Waiting for group to become stable, current operations: creating: 1
Group is stable
INSTANCE_GROUPS=kubernetes-minion-group
NODE_NAMES=kubernetes-minion-group-4ppl kubernetes-minion-group-mtpt kubernetes-minion-group-tqvv
Trying to find master named 'kubernetes-master'
Looking for address 'kubernetes-master-ip'
Using master: kubernetes-master (external IP: 35.188.206.177)
Waiting up to 300 seconds for cluster initialization.
  This will continually check to see if the API for kubernetes is reachable.
  This may time out if there was some uncaught error during start up.
...........Kubernetes cluster created.
Cluster "spheric-temple-187614_kubernetes" set.
User "spheric-temple-187614_kubernetes" set.
Context "spheric-temple-187614_kubernetes" created.
Switched to context "spheric-temple-187614_kubernetes".
User "spheric-temple-187614_kubernetes-basic-auth" set.
Wrote config for spheric-temple-187614_kubernetes to /home/babacoders/.kube/config
Kubernetes cluster is running.  The master is running at:
  https://35.188.206.177
  
... calling validate-cluster
Validating gce cluster, MULTIZONE=
Project: spheric-temple-187614
Network Project: spheric-temple-187614
Zone: us-central1-b
No resources found.
Waiting for 4 ready nodes. 0 ready nodes, 0 registered. Retrying.
No resources found.
Waiting for 4 ready nodes. 0 ready nodes, 0 registered. Retrying.
Waiting for 4 ready nodes. 0 ready nodes, 4 registered. Retrying.
Waiting for 4 ready nodes. 2 ready nodes, 4 registered. Retrying.
Found 4 node(s).
NAME                           STATUS                     ROLES     AGE       VERSION
kubernetes-master              Ready,SchedulingDisabled   <none>    37s       v1.9.3
kubernetes-minion-group-4ppl   Ready                      <none>    35s       v1.9.3
kubernetes-minion-group-mtpt   Ready                      <none>    38s       v1.9.3
kubernetes-minion-group-tqvv   Ready                      <none>    38s       v1.9.3
Validate output:
NAME                 STATUS    MESSAGE              ERROR
etcd-1               Healthy   {"health": "true"}   
etcd-0               Healthy   {"health": "true"}   
controller-manager   Healthy   ok                   
scheduler            Healthy   ok                   
Cluster validation succeeded
Done, listing cluster services:
Kubernetes master is running at https://35.188.206.177
GLBCDefaultBackend is running at https://35.188.206.177/api/v1/namespaces/kube-system/services/default-http-backend:http/proxy
Heapster is running at https://35.188.206.177/api/v1/namespaces/kube-system/services/heapster/proxy
KubeDNS is running at https://35.188.206.177/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
kubernetes-dashboard is running at https://35.188.206.177/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy
Metrics-server is running at https://35.188.206.177/api/v1/namespaces/kube-system/services/https:metrics-server:/proxy
Grafana is running at https://35.188.206.177/api/v1/namespaces/kube-system/services/monitoring-grafana/proxy
InfluxDB is running at https://35.188.206.177/api/v1/namespaces/kube-system/services/monitoring-influxdb:http/proxy
To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.
Kubernetes binaries at /home/babacoders/kubernetes/cluster/
You may want to add this directory to your PATH in $HOME/.profile
Installation successful!
```


```

$ kubernetes/cluster/kube-up.sh 
... Starting cluster in us-central1-b using provider gce
... calling verify-prereqs
... calling verify-kube-binaries
... calling kube-up
Project: spheric-temple-187614
Network Project: spheric-temple-187614
Zone: us-central1-b
+++ Staging server tars to Google Storage: gs://kubernetes-staging-99eb322adf/kubernetes-devel
+++ kubernetes-server-linux-amd64.tar.gz uploaded earlier, cloud and local file md5 match (md5 = c2a70c36601997cc02cc092bb0651bc4)
+++ kubernetes-salt.tar.gz uploaded earlier, cloud and local file md5 match (md5 = 667ac778e8135a040299eff91dceb486)
+++ kubernetes-manifests.tar.gz uploaded earlier, cloud and local file md5 match (md5 = c53b6b8a460e6fbefce10c2636cafc71)
INSTANCE_GROUPS=kubernetes-minion-group
NODE_NAMES=kubernetes-minion-group-4ppl kubernetes-minion-group-mtpt kubernetes-minion-group-tqvv
Looking for already existing resources
Managed instance groups kubernetes-minion-group found.
Would you like to shut down the old cluster (call kube-down)? [y/N] y
... calling kube-down
INSTANCE_GROUPS=kubernetes-minion-group
NODE_NAMES=kubernetes-minion-group-4ppl kubernetes-minion-group-mtpt kubernetes-minion-group-tqvv
Bringing down cluster
Deleting autoscalers...
done.
Deleting Managed Instance Group...
..............................Deleted [https://www.googleapis.com/compute/v1/projects/spheric-temple-187614/zones/us-central1-b/instanceGroupManagers
/kubernetes-minion-group].
done.
Deleted [https://www.googleapis.com/compute/v1/projects/spheric-temple-187614/global/instanceTemplates/kubernetes-minion-template].
WARNING: The public SSH key file for gcloud does not exist.
WARNING: The private SSH key file for gcloud does not exist.
WARNING: You do not have an SSH key for gcloud.
WARNING: SSH keygen will be executed to generate a key.
Generating public/private rsa key pair.
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /home/babacoders/.ssh/google_compute_engine.
Your public key has been saved in /home/babacoders/.ssh/google_compute_engine.pub.
........Creating firewall...
.Created [https://www.googleapis.com/compute/v1/projects/spheric-temple-187614/global/firewalls/kubernetes-default-internal-master].
.done.
NAME                                NETWORK  DIRECTION  PRIORITY  ALLOW                                       DENY
kubernetes-default-internal-master  default  INGRESS    1000      tcp:1-2379,tcp:2382-65535,udp:1-65535,icmp
................Created [https://www.googleapis.com/compute/v1/projects/spheric-temple-187614/regions/us-central1/addresses/kubernetes-master-ip].
Created [https://www.googleapis.com/compute/v1/projects/spheric-temple-187614/global/firewalls/kubernetes-master-https].
.done.
.NAME                     NETWORK  DIRECTION  PRIORITY  ALLOW    DENY
kubernetes-master-https  default  INGRESS    1000      tcp:443
.....Generating certs for alternate-names: IP:104.198.234.137,IP:10.0.0.1,DNS:kubernetes,DNS:kubernetes.default,DNS:kubernetes.default.svc,DNS:kubern
etes.default.svc.cluster.local,DNS:kubernetes-master
Created [https://www.googleapis.com/compute/v1/projects/spheric-temple-187614/global/firewalls/kubernetes-default-internal-node].
.done.
NAME                              NETWORK  DIRECTION  PRIORITY  ALLOW                         DENY
kubernetes-default-internal-node  default  INGRESS    1000      tcp:1-65535,udp:1-65535,icmp
..Created [https://www.googleapis.com/compute/v1/projects/spheric-temple-187614/global/firewalls/default-default-ssh].
done.
NAME                 NETWORK  DIRECTION  PRIORITY  ALLOW   DENY
default-default-ssh  default  INGRESS    1000      tcp:22
...Created [https://www.googleapis.com/compute/v1/projects/spheric-temple-187614/global/firewalls/kubernetes-master-etcd].
done.
NAME                    NETWORK  DIRECTION  PRIORITY  ALLOW              DENY
kubernetes-master-etcd  default  INGRESS    1000      tcp:2380,tcp:2381
Unable to successfully run 'cfssl' from /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin; downloadi
ng instead...
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  9.8M  100  9.8M    0     0  3377k      0  0:00:03  0:00:03 --:--:-- 2754k
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 2224k  100 2224k    0     0  1112k      0  0:00:02  0:00:02 --:--:--  923k
2018/02/14 17:46:47 [INFO] generating a new CA key and certificate from CSR
2018/02/14 17:46:47 [INFO] generate received request
2018/02/14 17:46:47 [INFO] received CSR
2018/02/14 17:46:47 [INFO] generating key: ecdsa-256
2018/02/14 17:46:47 [INFO] encoded CSR
2018/02/14 17:46:47 [INFO] signed certificate with serial number 203747428689453857117037706517252432359514702440
Generate peer certificates...
2018/02/14 17:46:47 [INFO] generate received request
2018/02/14 17:46:47 [INFO] received CSR
2018/02/14 17:46:47 [INFO] generating key: ecdsa-256
2018/02/14 17:46:47 [INFO] encoded CSR
2018/02/14 17:46:47 [INFO] signed certificate with serial number 224634586514214780058790458476308792862224276601
+++ Logging using Fluentd to gcp
Creating firewall...
...........Created [https://www.googleapis.com/compute/v1/projects/spheric-temple-187614/global/firewalls/kubernetes-minion-all].
done.
NAME                   NETWORK  DIRECTION  PRIORITY  ALLOW                     DENY
kubernetes-minion-all  default  INGRESS    1000      tcp,udp,icmp,esp,ah,sctp
WARNING: You have selected a disk size of under [200GB]. This may result in poor I/O performance. For more information, see: https://developers.google.com/compute/docs/disks#performance.
Created [https://www.googleapis.com/compute/v1/projects/spheric-temple-187614/zones/us-central1-b/instances/kubernetes-master].
NAME               ZONE           MACHINE_TYPE   PREEMPTIBLE  INTERNAL_IP  EXTERNAL_IP      STATUS
kubernetes-master  us-central1-b  n1-standard-1               10.128.0.2   104.198.234.137  RUNNING
Creating nodes.
Using subnet default
Attempt 1 to create kubernetes-minion-template
WARNING: You have selected a disk size of under [200GB]. This may result in poor I/O performance. For more information, see: https://developers.google.com/compute/docs/disks#performance.
Created [https://www.googleapis.com/compute/v1/projects/spheric-temple-187614/global/instanceTemplates/kubernetes-minion-template].
NAME                        MACHINE_TYPE   PREEMPTIBLE  CREATION_TIMESTAMP
kubernetes-minion-template  n1-standard-2               2018-02-14T09:47:10.645-08:00
Created [https://www.googleapis.com/compute/v1/projects/spheric-temple-187614/zones/us-central1-b/instanceGroupManagers/kubernetes-minion-group].
NAME                     LOCATION       SCOPE  BASE_INSTANCE_NAME       SIZE  TARGET_SIZE  INSTANCE_TEMPLATE           AUTOSCALED
kubernetes-minion-group  us-central1-b  zone   kubernetes-minion-group  0     3            kubernetes-minion-template  no
Waiting for group to become stable, current operations: creating: 3
Group is stable
INSTANCE_GROUPS=kubernetes-minion-group
NODE_NAMES=kubernetes-minion-group-39rs kubernetes-minion-group-3f46 kubernetes-minion-group-3fpc
Trying to find master named 'kubernetes-master'
Looking for address 'kubernetes-master-ip'
Using master: kubernetes-master (external IP: 104.198.234.137)
Waiting up to 300 seconds for cluster initialization.

  This will continually check to see if the API for kubernetes is reachable.
  This may time out if there was some uncaught error during start up.

..............Kubernetes cluster created.
Cluster "spheric-temple-187614_kubernetes" set.
User "spheric-temple-187614_kubernetes" set.
Context "spheric-temple-187614_kubernetes" created.
Switched to context "spheric-temple-187614_kubernetes".
User "spheric-temple-187614_kubernetes-basic-auth" set.
Wrote config for spheric-temple-187614_kubernetes to /home/babacoders/.kube/config
Kubernetes cluster is running.  The master is running at:
2018/02/14 17:46:47 [INFO] encoded CSR
2018/02/14 17:46:47 [INFO] signed certificate with serial number 224634586514214780058790458476308792862224276601
+++ Logging using Fluentd to gcp
Creating firewall...
...........Created [https://www.googleapis.com/compute/v1/projects/spheric-temple-187614/global/firewalls/kubernetes-minion-all].
done.
NAME                   NETWORK  DIRECTION  PRIORITY  ALLOW                     DENY
kubernetes-minion-all  default  INGRESS    1000      tcp,udp,icmp,esp,ah,sctp
WARNING: You have selected a disk size of under [200GB]. This may result in poor I/O performance. For more information, see: https://developers.googl
e.com/compute/docs/disks#performance.
Created [https://www.googleapis.com/compute/v1/projects/spheric-temple-187614/zones/us-central1-b/instances/kubernetes-master].
NAME               ZONE           MACHINE_TYPE   PREEMPTIBLE  INTERNAL_IP  EXTERNAL_IP      STATUS
kubernetes-master  us-central1-b  n1-standard-1               10.128.0.2   104.198.234.137  RUNNING
Creating nodes.
Using subnet default
Attempt 1 to create kubernetes-minion-template
WARNING: You have selected a disk size of under [200GB]. This may result in poor I/O performance. For more information, see: https://developers.googl
e.com/compute/docs/disks#performance.
Created [https://www.googleapis.com/compute/v1/projects/spheric-temple-187614/global/instanceTemplates/kubernetes-minion-template].
NAME                        MACHINE_TYPE   PREEMPTIBLE  CREATION_TIMESTAMP
kubernetes-minion-template  n1-standard-2               2018-02-14T09:47:10.645-08:00
Created [https://www.googleapis.com/compute/v1/projects/spheric-temple-187614/zones/us-central1-b/instanceGroupManagers/kubernetes-minion-group].
NAME                     LOCATION       SCOPE  BASE_INSTANCE_NAME       SIZE  TARGET_SIZE  INSTANCE_TEMPLATE           AUTOSCALED
kubernetes-minion-group  us-central1-b  zone   kubernetes-minion-group  0     3            kubernetes-minion-template  no
Waiting for group to become stable, current operations: creating: 3
Group is stable
INSTANCE_GROUPS=kubernetes-minion-group
NODE_NAMES=kubernetes-minion-group-39rs kubernetes-minion-group-3f46 kubernetes-minion-group-3fpc
Trying to find master named 'kubernetes-master'
Looking for address 'kubernetes-master-ip'
Using master: kubernetes-master (external IP: 104.198.234.137)
Waiting up to 300 seconds for cluster initialization.
  This will continually check to see if the API for kubernetes is reachable.
  This may time out if there was some uncaught error during start up.
..............Kubernetes cluster created.
Cluster "spheric-temple-187614_kubernetes" set.
User "spheric-temple-187614_kubernetes" set.
Context "spheric-temple-187614_kubernetes" created.
Switched to context "spheric-temple-187614_kubernetes".
User "spheric-temple-187614_kubernetes-basic-auth" set.
Wrote config for spheric-temple-187614_kubernetes to /home/babacoders/.kube/config
Kubernetes cluster is running.  The master is running at:
https://104.198.234.137
The user name and password to use is located in /home/babacoders/.kube/config.
... calling validate-cluster
Validating gce cluster, MULTIZONE=
Project: spheric-temple-187614
Network Project: spheric-temple-187614
Zone: us-central1-b
No resources found.
Waiting for 4 ready nodes. 0 ready nodes, 0 registered. Retrying.
No resources found.
Waiting for 4 ready nodes. 0 ready nodes, 0 registered. Retrying.
Waiting for 4 ready nodes. 0 ready nodes, 1 registered. Retrying.
Waiting for 4 ready nodes. 0 ready nodes, 4 registered. Retrying.
Found 4 node(s).
NAME                           STATUS                     ROLES     AGE       VERSION
kubernetes-master              Ready,SchedulingDisabled   <none>    37s       v1.9.3
kubernetes-minion-group-39rs   Ready                      <none>    31s       v1.9.3
kubernetes-minion-group-3f46   Ready                      <none>    26s       v1.9.3
kubernetes-minion-group-3fpc   Ready                      <none>    27s       v1.9.3
Validate output:
NAME                 STATUS    MESSAGE              ERROR
etcd-1               Healthy   {"health": "true"}   
scheduler            Healthy   ok                   
controller-manager   Healthy   ok                   
etcd-0               Healthy   {"health": "true"}   
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
