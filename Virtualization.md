# Virtualization

## What is virtualization:

- Virtualization is technology that enables the creation of virtual envirements from single pyhisical machine, allowing for more efficient use of resources by distributing them  across computing enviroments.[^1]

- Using software, virtualization creates an abstraction layer over computer hardware, dividing a single system's components such as processors, memory, network and storage into multiple **virtual machines (VMs)**. Each VM runs its own **operating system (OS)** and behaves like separate physical computer, despite the same underlying hardware.[^1]

- The software layer that does this abstraction is usually called **hypervisor**. the hypervisor allocates and manages the physical server.

![The architecture of Virtualization](https://www.techtarget.com/rms/onlineimages/virtual_machines-h.png "image of the architecture")

## The role of hypervisor:

- The hypervisor manages resources and allocates them the VMs. it also schedules and adjasts how resources are distributed based on the configuration of the hypervisor, including reallocating resources as demand fluctuate.[^2]

- The hypervisor emulates teh computer's CPU, memor, hard disk, network, and other hardware resources, creating a pool of resources for each individual VMs.

- Most hypervisor fall into one of two categories: 
    - Type1 hypervisor: Also knowen as **bare-metal hypervisor**. Runs directly on the physical host machine and have direct access to its hardware. It runs on **server** computers and are considered more efficient and better performing than type 2 hypervisor, making them well-suited to server, desktop and application virtualization. Example of type 1 hypervisor is _Microsoft Hyper-V_.[^2]
    - Type2 hypervisor: also knowen as **hosted hypervisor**. Installe on top of the hiost machine's OS, which manages calls to the hardware resources. Type 2 hypervisor are generally deployed on end-user systems for specific use cases. Example of type 2 hypervisor is _VMware Workstation_ and _Oracle VirtualBox_.[^2]
[^1]: https://www.ibm.com/think/topics/virtualization
[^2]: https://www.techtarget.com/searchitoperations/definition/virtual-machine-VM
