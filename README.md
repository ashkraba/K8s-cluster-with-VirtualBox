# K8s cluster for testing

This ansible roles help you create local k8s cluster with one master node and one worker node to VirtualBox infrastructure. What this roles do:

  - Disable Selinux, swap and Firewalld
  - Install ntpdate package and synchronize time for hosts
  - Install iptables and configure rules for it
  - Create user for docker and k8s
  - Install docker and k8s to all hosts
  - Initialize k8s cluster and join node to it
  - Deploy CNI 

# IMPORTANT! Before using this roles:

  - please configure hostnames for your hosts. The result of the next command should return correct ip address of the host
    ```sh
    $ hostname -i
    ```
  - please sinchronize date and time for all your hosts (preparation role can failed if ntpdate port is in use)
  - master node should have at least 2 CPU and 2Gb of memory
  - change hosts in hosts.txt file according to your environment

You can also:
  - change a lot of default variables in every appropriate file for every role
  - use only the roles you need, roles are independent

# Requirements:
 - by default this cluster use [Calico](https://www.projectcalico.org/) as a CNI, but you can change it in defaults file.
 - role iptables open onle default ports for k8s and default ssh port, and close all other inpur rules
 - default user for docker and k8s is "test", and config file for kubectl added only for this user (not for root) 

# Notes:
All this roles was tested on default VirtualBox virtual machines with CentOS. If you found any mistakes please let me know. I hope this roles help you and save some working time.
I have tested this roles on GCP with CentOS 7 images and it works fine, but you need change apiserver-advertise-address in master_k8s role, because GCP engines use two network adapters (internal and external).

