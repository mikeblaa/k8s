# k8s
Repository to manage my Kubernetes learning and projects

## OKD
With Red Hat OpenShift being a leading commercial Kubernetes distribution, I wanted to start my learning with the open-source OKD project. To get started, I wanted to find a walk through aimed at installing OKD on a VMware server. This is the walk through I followed: https://itnext.io/guide-installing-an-okd-4-5-cluster-508a2631cbee

The primary constraint I have to work with is a limited amount of RAM. The server I intend to install OKD on has 32 GB of RAM. The guide, as written, calls for 8 seperate VMs with a total memory footprint of 101 GB! This forced me to adjust downward the number of VMs and the RAM assigned to each VM. I learned the OKD is very sensitive the amount of memory available. Through experimentation I determined the minimum amount of memory I could get away with. The table below captures the memory configurations that were successful and unsuccessful.

Server Motherboard: Asus Maximus VII Hero LGA 1150 Intel Z97<br>
Server Processor: Intel Core i7-4790 Haswell Quad-Core 3.6GHz<br>
Server Memory: 32 GB<br>
VMware ESXi version: 7.0.0<br>
OKD version: 4.5.0-0.okd-2020-10-15-235428

| controlPlane:<br>replicas: | compute:<br>replicas: | mastersSchedulable: | controlPlane Memory | compute Memory | Bootstrap Time | Console Available | Monitoring Available |
|----------------------------|-----------------------|---------------------|---------------------|----------------|----------------|-------------------|----------------------|
| 1                          | 0                     | true                | 8 GB                | N/A            | 14m17s         | False             | False                |
| 1                          | 0                     | true                | 12 GB               | N/A            | 12m24s         | True (15m)        | True (15m)           |
| 1                          | 0                     | true                | 16 GB               | N/A            | 14m48s         | True (14m)        | True (15m)           |
| 1                          | 1                     | false               | 16 GB               | 8 GB           |  9m57s         | True (13m)        | True (10m)           |
| 1                          | 2                     | false               | 16 GB               | 8 GB           |                |                   |                      |

Some useful commands
```
coreos.inst.install_dev=/dev/sda coreos.inst.image_url=http://192.168.1.210:8080/okd4/fcos.raw.xz coreos.inst.ignition_url=http://192.168.1.210:8080/okd4/bootstrap.ign
coreos.inst.install_dev=/dev/sda coreos.inst.image_url=http://192.168.1.210:8080/okd4/fcos.raw.xz coreos.inst.ignition_url=http://192.168.1.210:8080/okd4/master.ign
coreos.inst.install_dev=/dev/sda coreos.inst.image_url=http://192.168.1.210:8080/okd4/fcos.raw.xz coreos.inst.ignition_url=http://192.168.1.210:8080/okd4/worker.ign
openshift-install --dir=install_dir/ wait-for bootstrap-complete --log-level=info
watch -d oc get clusteroperators
watch -d oc get nodes
oc get csr
for i in $(oc get csr | awk '{ print $1 }'); do oc adm certificate approve $i; done;
```
