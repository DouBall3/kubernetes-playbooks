kubernetes-playbooks
=============

Ansible playbooks that creates a Kubernetes cluster of Raspberry PIs running Ubuntu 24.04.

## Prerequisites
* Ansible and Python3 installed on the local machine (`# yum install ansible`).

## Create an inventory file for Ansible

A `hosts` file can be created. Add the IP address to the master and workers in the `hosts` file using a text editor, and make sure each machine can be reached using SSH:

 `$ cp hosts.example hosts`

 `$ vim hosts`

## Install Kubernetes dependencies on all servers
 `$ ansible-playbook -i hosts playbooks/kube-dependencies.yml`

## Initialize the master node
 `$ ansible-playbook -i hosts playbooks/master.yml`

`ssh` onto the master and verify that the master node get status `Ready`:
```
$ ssh <username>@<master_ip>
ubuntu@k8s-master-1:~$ kubectl get nodes
NAME           STATUS   ROLES           AGE   VERSION
k8s-master-1   Ready    control-plane   30s   v1.29.0
```

## Add the worker nodes
 `$ ansible-playbook -i hosts playbooks/workers.yml`

Run `kubectl get nodes` once more on the master node to verify the worker nodes got added.

## Install cilium network
 `$ ansible-playbook -i hosts playbooks/network.yml`


## Credits
Based on torgeirl's «[kubernetes-playbooks](https://github.com/torgeirl/kubernetes-playbooks)».

## License
See the [LICENSE](LICENSE.md) file for license rights and limitations (MIT).
