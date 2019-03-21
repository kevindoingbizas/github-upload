# Openshift Hardening
The set of playbooks in this repository complete the hardening recommendations for Openshift Container Platform 3.10 and 3.11.

## Example Execution
To run a majority of roles you can run when in the ocp-hardening-ansible/working directory::
ansible-playbook harden_cluster.yml

## Roles Used
This playbook is the main playbook which imports and runs tasks from the roles in the working/roles directory.
There are four roles that complete hardening tasks:
secure-worker-nodes
sdn-networkpolicy
lockdown-ocp
configuration-files-all-nodes

## Description of Roles and how they are run in harden_cluster.yml
The secure-worker-nodes role changes the node-config-maps for compute nodes.

The sdn-networkpolicy role changes the sdn of the cluster to network policy and changes node-config-maps
and config files for the master, compute, and infra nodes. It also restarts the master api and controllers.
Currently there are also four extra playbooks (sdn-configmap.yml, sdn-masterconfig.yml, sdn-node-services.yml, sdn-services.yml) which are under the working directory. These playbooks need to be tested and can then replace most of the playbooks in this role.

The lockdown-ocp role changes many of the configuration files on the master nodes. 

The configuration-files-all-nodes role changes permissions for the /etc/origin/openvswitch/ and /etc/cni/net.d/ directories on all nodes. 

The harden_cluster.yml playbook before running any of the tasks from these roles saves a backup copy of the master-config.yaml and master.env files. Currently all but the sdn-networkpolicy roles are being used. There are tasks in the secure-work-nodes role that update the sdn policy and restart the node service.
The sdn-networkpolicy role will be updated to use the four aforementioned sdn- playbooks. 
