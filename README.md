inspired by:
  - https://github.com/coreos/coreos-vagrant.git
  - https://github.com/coreos/coreos-kubernetes/blob/master/multi-node/vagrant/Vagrantfile


## Differences:

- Allow setting up etcd without discovery service (static configuration)
- Allow setting up an n-node etcd cluster using vagrant by autodetecting the number of instances started


## Usage:

### Start 3-node cluster

	$ NUM_INSTANCES=3 vagrant up

### Add node to the cluster

	$ NUM_INSTANCES=4 vagrant ssh etcd-01
	etcd-01$ sudo etcdctl member add etcd-04 http://172.17.8.104:2380
	etcd-01$ exit
	$ NUM_INSTANCES=4 ACTION=add vagrant up etcd-04