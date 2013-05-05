#### Introduction

These example playbooks should be a good reference point for using riakcs with ansible.  These playbooks were tested on Ubuntu Precise (12.04).

#### Hosts File Naming Conventions

In the hosts file, we use a host variable **node_type** to ease the cluster joining process.  The following values of **node_type** can be used.

* **primary** - all nodes attempt to join this node.
* **last** - this node plans and commits changes to the cluster, in this example, the joining of the nodes.  
* **middle** - all nodes in between **primary** and **last**


**Groups**

* **riakcs_cluster** - members of the riakcs cluster you want to build
* **stanchion** - one or servers are designated to be the stanchion servers.
* **localhost** - the loopback ip, use for updating CS admin credentials to a local file.


You can build an entire cluster by first modifying the hosts file to fit your
network.

#### Using the Playbooks

Here are the playbooks that you can use with the ansible-playbook commands:

* **site.yml** - creates a complete riak-cs cluster with haproxy and a s3cfg file locally at /tmp/ansible-s3cfg
* **install_riakcs.yml** - installs riak onto the cluster
* **install_stanchion.yml** - installs stanchion
* **reset_creds.yml** - resets the riakcs admin credentials, updates the group_vars/all file with the new credentials, and updates all nodes with new credentials.
* **rolling_restart.yml** - demonstrates the ability to perform a rolling CS configuration change.


Creating the cluster for the first time is a 2 step process

	ansible-playbook site.yml
	ansible-playbook reset_creds.yml
	
The first step will deploy riak, stanchion, and riakcs and create a cluster.  The second step will set up the riakcs credentails in stanchion and riakcs.

You should only run reset_creds.yml when you want the credentials reset!


#### Using Riak CS

put a file:

	s3cmd  -c /tmp/s3cfg-ansible mb s3://test
    s3cmd -c /tmp/s3cfg-ansible put /tmp/myfile s3://test
    
get a file:

    s3cmd -c /tmp/s3cfg-ansible get s3://test/myfile