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

| controlPlane:<br>replicas: | compute:<br>replicas: | mastersSchedulable: | controlPlane Memory | computer Memory | Result                        |
|----------------------------|-----------------------|---------------------|---------------------|-----------------|-------------------------------|
| 1                          | 0                     | true                | 8 GB                | N/A             | Bootstrap complete: 14m17s<br>Console available: Never comes up<br>Monitoring available: Never comes up|
| 1                          | 0                     | true                | 12 GB               | N/A             | Bootstrap complete: 12m24s<br>Console available: 15m<br>Monitoring available: 15m|
| 1                          | 0                     | true                | 16 GB               | N/A             | Bootstrap complete: 14m48s<br>Console available: 14m<br>Monitoring available: 15m |
| 1                          | 2                     | false               | 8 GB                | 4 GB            | Console available in xxx mins |
| 1                          | 2                     | false               | 12 GB               | 4 GB            | Console available in xxx mins |
| 1                          | 2                     | false               | 16 GB               | 4 GB            | Console available in xxx mins |
