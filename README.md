# k8s
Repository to manage my Kubernetes learning and projects

## OKD
With Red Hat OpenShift being a leading commercial Kubernetes distribution, I wanted to start my learning with the open-source OKD project. To get started, I wanted to find a walk through aimed at installing OKD on a VMware server. This is the walk through I followed: https://itnext.io/guide-installing-an-okd-4-5-cluster-508a2631cbee

The primary constraint I have to work with is a limited amount of RAM. The server I intend to install OKD on has 32 GB of RAM. The guide, as written, calls for 8 seperate VMs with a total memory footprint of 101 GB! This forced me to adjust downward the number of VMs and the RAM assigned to each VM. I learned the OKD is very sensitive the amount of memory available. Through experimentation I determined the minimum amount of memory I could get away with. The table below captures the memory configurations that were successful and unsuccessful.
