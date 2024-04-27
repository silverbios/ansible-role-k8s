K8S-Multi-Master
================

This role installs K8S 1.29 version with external etcd, which has a multi-master feature in K8S and redundancy for the etcd cluster with Cilium as CNI.

Requirements
------------

At least three master nodes are needed to use the K8S master and etcd cluster simultaneously.

This Role is based on the Linux with Ubuntu distro, Jammy version.

In this role, I disabled kube-proxy during cluster initialization and using cilium, so you should use at least Linux kernel v.4.19.57


# Setup
To up and run this kind of cluster, after cloning the repo, you should run the playbook something like the below:

```yaml
- hosts: "k8s_masters, k8s_workers, k8s_utils"
  become: yes
  become_user: root
  become_method: sudo
  gather_facts: yes
  vars_prompt:
    - name: "ansible_become_pass"
      prompt: "Enter sudo password"
      private: yes

  roles:
    - k8s_setup
```


Beware: If you are connecting to your node via SSH-PASS, you should pass the "-k" option in the playbook command to Ansible to get the SSH password from you.