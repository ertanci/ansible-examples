#### Introduction

These example playbooks should be a good reference point for using riakcs with ansible.  These playbooks were tested on Ubuntu Precise (12.04).

#### Hosts File Naming Conventions

In the hosts file, we define the different groups to ease the cluster joining process. This is very similar to the example playbook for the riak cluster.

* **riakcluster_primary** - all nodes attempt to join this node. There should only be one member of this group.
* **riakcluster_last** - this node plans and commits changes to the cluster, in this example, the joining of the nodes.  
* **riakcluster_middle** - all nodes in between are members of this group.


**Groups**

* **riakcs_cluster** - members of the riakcs cluster you want to build
* **stanchion** - one or servers are designated to be the stanchion servers.
* **riak_cluster** - used as an alias for compatibility with riak playbooks
* **localhost** - the loopback ip, use for updating CS admin credentials to a local file.


You can build an entire cluster by first modifying the hosts file to fit your
network.

#### Using the Playbooks

Here are the playbooks that you can use with the ansible-playbook commands:

* **site.yml** - creates a complete riak-cs cluster.
* **install_riakcs.yml** - installs riak onto the cluster
* **install_stanchion.yml** - installs stanchion
* **reset_admin_creds.yml** - resets the riakcs admin credentials, updates the group_vars/all file with the new credentials, and updates all nodes with new credentials.
* **rolling_restart.yml** - demonstrates the ability to perform a rolling
configuration change.  Similar principals could apply to performing
rolling upgrades of Riak itself.


Creating the cluster for the first time is a 2 step process

	ansible-playbook site.yml
	ansible-playbook playbooks/reset_admin_creds.yml
	
The first step will deploy riak, stanchion, and riakcs and create a cluster.  The second step will set up the riakcs credentails in stanchion and riakcs.

You should only run reset_admin_creds.yml when you want the credentials reset!