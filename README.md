# exam-aug-16-2021

## Docker in production (50 points)

Given the Linkup game https://drive.google.com/file/d/1FPyinDVS8lxk7tRp998N_rJ8PgvqhhEv/view?usp=sharing
Put the game in a container using docker-compose.yml and push ALL the images to your personal docker hub account.
Add telemetry in your docker-compose using the ff:

* prometheus
* alertmanager
* grafana
* node exporter
* cadvisor (Container Advisor)

Submit the ff files through email:

* Dockerfile of the linkup game
* docker-compose.yml file
* screenshot of linkup game
* screenshot of prometheus targets
* screenshot of cadvisor
* screenshot of grafana docker host dashboard

Optional:
Check your docker-compose.yml file using https://www.docker.com/play-with-docker Lab

## kubernetes

* you are allocated 2 servers. Change the hostnames of both servers to:
  * (yourname)-master
  * (yourname)-worker
* for each node, edit /root/.bashrc to contain:


```
HISTSIZE=1000000
HISTIGNORE="ls:ll:pwd:bg:fg:history"
HISTCONTROL=ignoreboth:erasedups
HISTTIMEFORMAT="%d/%m/%y %T "
```

* install the following packages: net-tools bind-utils tc firewalld git
* install a kubernetes cluster as per https://www.tecmint.com/install-a-kubernetes-cluster-on-centos-8/. One master and one worker node.
  * NOTE: before you start the kubelet, run this command:

```
echo "KUBELET_EXTRA_ARGS=--cgroup-driver=cgroupfs" > /etc/sysconfig/kubelet
```

* if you wish to restart the kubernetes installation, do it with

```
kubeadm reset --force; rm -rf /etc/cni/net.d/
```

* on the newly created cluster, create your namespace called (yourname)
* on the master node in the /root directory, clone the git repository https://github.com/microservices-demo/microservices-demo
* edit deploy/kubernetes/complete-demo.yaml - ensure that all resources are going to be created under your namespace

```
apiVersion: v1
kind: Namespace
metadata:
  name: sock-shop  <-- change to (yourname)
...
namespace: sock-shop <-- replace all occurences to (yourname)
```
* apply the modified deploy/kubernetes/complete-demo.yaml file.
* ensure that your application is accesible from http://(public ip):(service port). run `kubectl get service --namespace (yourname)` to check the service port of the microservice called *frontend*
