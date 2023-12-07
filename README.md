# Welcome to the YAVAK (Yet another Vagrant Ansible Kube) Playbooks

Small project to quickly deploy an MVP Kube cluster using Fedora, vagrant, and ansible. Most of the current playbooks use Docker, Ubuntu
or another not so native Fedora/RH component to work. I like staying in the RH ecosystem so YAVAK's goal was to be able to take Fedora thumbdrive and go from zero to an kubernetes cluster without needing lots of extra non-Fedora repos.

Currently it has been test on Fedora 37-39 to host clusters and additionally RHEL9 can acts as ansible controller..

## Using Project

To use the playbooks the ansible controller needs to have the following installed

 - ansible 
 - ansible-core 
 - python3-xmltodict

The Ansible remote-user needs to have the ability to sudo to execute certian system tasks such as install new packages. The playbook is desing to work targeting either the localhost or a remote server to install Vagrant establish a "master" node and "working" nodes, currently limited to 1 of each. Target vagrant needs atleast 4 cores and 6 gig of ram. The complete cluster will provide a minimum setup of kubernetes, calico and kubernetes-dashboard. Planned supplemental playbooks will install metrics-server. 

#### A note about installing kubernetes with rpms

A note about the Kubernetes rpms in Fedora F37, F38, and F39 (potential change in F40). Most of the Kube docs for Fedora run to the very old ( so lots of changes and the Interweb forgets nothing), so this will proivde some in sight on to the process used here.

>The kubernetes-node rpm installs kubelet.
>
>The kubernetes-kubeadm rpm installs kubeadm.
>
>The kubernetes-client rpm installs kubectl.
>
>The kubernetes-master rpm installs as systemd units kube-proxy, kube-apiserver, and kube-scheduler. This rpm and these systemd units are only needed if you are following the Kubernetes The Hard Way tutorial (GitHub - kelseyhightower/kubernetes-the-hard-way: Bootstrap Kubernetes the hard way on Google Cloud Platform. No scripts. 8). Otherwise this rpm is not needed.
>
>If using kubeadm to initialize a cluster, these services are installed as static pods on the control plane so the systemd units are not needed.
>
>At this time the kubernetes-node rpm also will require either cri-o or containerd be installed. 

This playbook use cri-o as the container engine
