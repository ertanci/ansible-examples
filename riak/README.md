#### Introduction

These example playbooks should help you get an idea of how to use the riak ansible module.  These playbooks were tested on Ubuntu Precise (12.04).

#### Hosts File Naming Conventions

In the hosts file, we use a host variable **node_type** to ease the cluster joining process.  The following values of **node_type** can be used.

* **primary** - all nodes attempt to join this node.
* **last** - this node plans and commits changes to the cluster, in this example, the joining of the nodes.  
* **middle** - all nodes in between **primary** and **last**

 
There is no concept of node roles in Riak proper, it is master-less.

You can build an entire cluster by first modifying the hosts file to fit your
network.

#### Using the Playbooks

Here are the playbooks that you can use with the ansible-playbook commands:

* **site.yaml** - creates a complete riak cluster, it calls install_riak.yaml and form_cluster.yaml
* **install_riak.yaml** - tunes the operating system and installs Riak
* **form_cluster.yaml** - forms a riak cluster
* **rolling_restart.yaml** - demonstrates the ability to perform a rolling
configuration change.  Similar principals could apply to performing
rolling upgrades of Riak itself.

