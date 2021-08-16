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

## kubernetes (50 points)

* you are allocated 2 servers. Change the hostnames of both servers to:
  * (yourname)-master
  * (yourname)-worker
* you will receive the server information and credentials via pm.
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

* on the newly created cluster, create your own namespace called (yourname)
* on the master node in the /root directory, clone the git repository https://github.com/microservices-demo/microservices-demo
* edit deploy/kubernetes/complete-demo.yaml - ensure that all resources are going to be created under your namespace
  * example:
```
apiVersion: v1
kind: Namespace
metadata:
  name: sock-shop  <-- change to (yourname)
...
namespace: sock-shop <-- replace all occurences to (yourname)
```

* apply the modified deploy/kubernetes/complete-demo.yaml file. 
* check the status of the services. [take note of the service called *front-end*](https://user-images.githubusercontent.com/87228894/129575405-b1826c76-5f49-4f5a-86df-9f2a8be0c8de.png)
* it is possible that not all of the microservices are going to run. Atleast ensure that [*front-end* is running](https://imgur.com/n5luwkY). Bonus 10 points if you can get all services to run.
* ensure that your application is accesible from http://(public ip):(service port). run `kubectl get service --namespace (yourname)` to check the service port of the microservice called *front-end*
* you should be able to browse the application [like this](https://imgur.com/6kq0bcT)
