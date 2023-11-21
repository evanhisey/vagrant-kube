# vagrant-kube

Small project to quickly deploy an MVP Kube cluster using Fedora, vagrant, and ansible. 

Currently it has been test on Fedora 37-39 to host clusters and additionally RHEL9 can acts as ansible controller..

## Using Project

To use the playbooks the ansible controller needs to have the following installed

 - ansible 
 - ansible-core 
 - python3-xmltodict

The Ansible remote-user needs to have the ability to sudo to execute certian system tasks such as install new packages. 

### A note about install kubernetes

A note about the Kubernetes rpms in Fedora F37, F38, and F39 (potential change in F40). Most of the Kub8 docs for fedora run to the very old ( lot so of changes and the Interweb forgets nothing), so this will proivde some in sight on to the process used here.
 
The kubernetes-node rpm installs kubelet.
The kubernetes-kubeadm rpm installs kubeadm.
The kubernetes-client rpm installs kubectl.

The kubernetes-master rpm installs as systemd units kube-proxy, kube-apiserver, and kube-scheduler. This rpm and these systemd units are only needed if you are following the Kubernetes The Hard Way tutorial (GitHub - kelseyhightower/kubernetes-the-hard-way: Bootstrap Kubernetes the hard way on Google Cloud Platform. No scripts. 8). Otherwise this rpm is not needed.

If using kubeadm to initialize a cluster, these services are installed as static pods on the control plane so the systemd units are not needed.

At this time the kubernetes-node rpm also will require either cri-o or containerd be installed.

The ansible playbooks and related scripts all follow the officila 