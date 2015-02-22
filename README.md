# kubernetes-coreos-cluster-vagrant

Setups up multi-node cluster using Kubernetes on CoreOS 

## Usage

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
