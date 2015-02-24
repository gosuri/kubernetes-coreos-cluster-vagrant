# kubernetes-coreos-cluster-vagrant

Setups up multi-node cluster using Kubernetes on CoreOS.

Derived from [User guide](https://github.com/pires/kubernetes-vagrant-coreos-cluster) and [guesbook](https://github.com/GoogleCloudPlatform/kubernetes/tree/master/examples/guestbook) example.

# Dependencies

**[Vagrant](https://www.vagrantup.com)**
**[Virtualbox](https://www.virtualbox.org)** 
**kubectl** (required to manage your kubernetes cluster)
**fleetctl** (optional for *debugging* **[fleet](http://github.com/coreos/fleet)**)
**etcdctl** (optional for *debugging* **[etcd](http://github.com/coreos/fleet)**)

On **MacOS X**:

```shell
$ brew install wget fleetctl etcdctl
```

# Usage

Bring up cluster using:

```shell
$ vagrant up
```

Set environment variables:

```shell
$(./shellinit)
```

List machines
```shell
$ fleetctl list-machines

MACHINE     IP            METADATA
22753cfd... 172.17.8.103  role=minion
244bb165... 172.17.8.101  role=master
7ba2e25d... 172.17.8.102  role=minion
```

## Redis master pod and service

Create redis master pod

```shell
kubectl create -f guestbook/redis-master.json
```

Create redis serivce - load balancer that proxies traffic to one or more containers.

```shell
kubectl create -f guestbook/redis-master-service.json
```

## Create redis slave pod and service

```shell
kubectl create -f guestbook/redis-slave-controller.json
kubectl create -f guestbook/redis-slave-service.json
```

## Create frontend pod and service
```shell
kubectl create -f guestbook/frontend-controller.json
kubectl create -f guestbook/frontend-service.json
```
