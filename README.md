inspired by:
  - https://github.com/coreos/coreos-vagrant.git
  - https://github.com/coreos/coreos-kubernetes/blob/master/multi-node/vagrant/Vagrantfile


## Differences:

- Allow setting up etcd without discovery service (static configuration)
- Allow setting up an n-node etcd cluster using vagrant by autodetecting the number of instances started


## Usage:

### Start 3-node etcd cluster

	$ export NUM_INSTANCES=3
	$ vagrant up
	
verify the cluster is healthy

	$ vagrant ssh etcd-02
	etcd-02$ etcdctl cluster-health
	member 48eff3d7ffd1ff6 is healthy: got healthy result from http://172.17.8.101:2379
	member 24fd8ea7cfccae5f is healthy: got healthy result from http://172.17.8.102:2379
	member e214c25dc73eafa9 is healthy: got healthy result from http://172.17.8.103:2379
	cluster is healthy

### Add node to the cluster

prepare cluster to receive new host

	$ NUM_INSTANCES=4 vagrant ssh etcd-01
	etcd-01$ sudo etcdctl member add etcd-04 http://172.17.8.104:2380

boot the new node with $ACTION="add" option

	$ NUM_INSTANCES=4 ACTION=add vagrant up etcd-04