<div align="center">


<!-- add technical charcha logo postgres session 3 -->
# Kubernetes Assignment 1        
### — A Task Documentation by Yash Anand —    

_____________________________________________________________________________________                        

## Contents
</div>

  - [**Overview**](#overview)
  - [**Prerequisites**](#prerequisites)
  - [**Task 1: Understanding Namespaces**](#task-1-understanding-namespaces)
  - [**Task 2: Learning Encoding \& Encryption**](#task-2-learning-encoding--encryption)
  - [**Task 3: Differentiating Tunnels \& Bridges**](#task-3-differentiating-tunnels--bridges)
    - [Tunneling In Networking](#tunneling-in-networking)
    - [Bridges In Networking](#bridges-in-networking)
  - [**Task 4: Understanding System Booting**](#task-4-understanding-system-booting)
  - [**Task 5: Modifying Podman's Data Directory**](#task-5-modifying-podmans-data-directory)
  - [**Task 6: Performing DO188 Guided Excercises**](#task-6-performing-do188-guided-excercises)
  - [**Task 6.1: Chapter 2 Guided Exercises**](#task-61-chapter-2-guided-exercises)
  - [**Task 6.1.1: Creating Containers with Podman**](#task-611-creating-containers-with-podman)
  - [**Task 6.1.2: Accessing Containerized Network Services**](#task-612-accessing-containerized-network-services)
  - [**Task 6.1.3: Accessing Containers**](#task-613-accessing-containers)
  - [**Task 6.1.4: Managing the Container Lifecycle**](#task-614-managing-the-container-lifecycle)
  - [**Conclusion**](#conclusion)
 
_____________________________________________________________________________________      
<div align="center">
   
# **Overview** 
</div>

In order to help gauge the understanding of the participants of the topics discussed in the first session on **`Kubernetes`**, we were assigned a total of 6 Tasks by Harsh Sir. The tasks assigned are mainly from the [Red Hat course of DO188](https://rol.redhat.com/rol/app/courses/do188-4.12/pages/pr01), which has been titled as **`Red Hat OpenShift Development I`**. Though the title of this course does not contain `Kuberenetes` in it, we can still understand its basics since OpenShift uses Kuberenetes underneath. 

During our first session, the chapters that we were able to cover as well as the chapters based on which we were assigned the tasks, were as follows:
-  Chapter 1: Introduction and Overview of Containers
-  Chapter 2: Podman Basics
-  Chapter 3: Container Images

<div align="center">     

![image](https://i.imgur.com/JN9QoAE.png)
   </div>

Through the means of this document, I will be providing answers and solutions to the assigned tasks, which are as follows:
- Learning Encoding & Encryption
- Differentiating Tunnels & Bridges
- Understanding System Booting
- Modifying Podman's Data Directory
- Performing DO188 Guided Excercises

Since the main objective of the first three chapters was to help the participants get a better understanding of Podman, I greatly utilised Tech Primers' tutorial that has been provided below before I got started with executing the assigned tasks: 

<div align="center">     

[![IMAGE_ALT](https://img.youtube.com/vi/Za2BqzeZjBk/maxresdefault.jpg)](https://www.youtube.com/watch?v=Za2BqzeZjBk)
   </div>

In the following sections, I have documented, demonstrated and explained how I was able to complete the assigned tasks that have been mentioned above, while using [Red Hat's DO188 Course](https://rol.redhat.com/rol/app/courses/do188-4.12/pages/pr01) as my main resource and guide. However, before being able to get started with the tasks, it was very much important to fulfill some prerequisites, which have been discussed in the next section.

<!-- yt links add krne de vaste:
0 or 1 or 2 or 3 or 4, 0 (big) to 4 (small)
hqdefault.jpg <- high quality
mqdefault.jpg <- medium quality
sddefault.jpg <- standard definition
maxresdefault.jpg <- maximum resolution -->

_____________________________________________________________________________________     

<div align="center">
   
## **Prerequisites**
</div>

Before I could get started with executing the assigned tasks, I needed to fulfill some preqrequisites, which only included logging into my Red Hat account and 
<div align="center">     

![image]()
   </div>

--------

<div align="center">

## **Task 1: Understanding Namespaces**
</div>

> Explain namespaces, their types & uses.   

Namespaces can be understood as enclosures that provide process and resuorce isolation. They allow different processes or containers to have their own view of various system resources, making it possible to run multiple instances of a resource without them interfering with each other. Linux namespaces are primarily used in containerization technologies like Docker and Kubernetes. Here are some common types of namespaces in Linux:

PID Namespace (Process ID Namespace): PID namespaces isolate the process IDs of a group of processes. Each namespace has its own set of process IDs, ensuring that processes in one namespace can't see or interfere with processes in another.

Mount Namespace: Mount namespaces provide an isolated view of the filesystem. Each namespace has its own mount points, so processes within a namespace can have a different view of the filesystem, even if they are running on the same physical machine.

Network Namespace: Network namespaces isolate network resources such as network interfaces, routing tables, and firewall rules. This allows each namespace to have its own network stack, making it possible to create separate network environments for different containers or processes.

UTS Namespace (Unix Time-Sharing Namespace): UTS namespaces isolate system identification information, such as the hostname and NIS (Network Information Service) domain name. This means each namespace can have its own hostname, making it appear as though different containers have different system identities.

IPC Namespace (Inter-Process Communication Namespace): IPC namespaces isolate System V IPC objects like message queues, semaphore sets, and shared memory segments. This prevents processes in one namespace from interfering with or accessing these objects in other namespaces.

User Namespace: User namespaces map user and group IDs inside a namespace to different IDs outside the namespace. This is crucial for security and allows a container, for example, to have its own user and group IDs while remaining isolated from the host system.

Cgroup Namespace: Cgroup namespaces provide isolation for control groups (cgroups), which are used for resource management and limiting resource usage by processes.

house with different rooms. Each room serves a specific purpose, such as a bedroom, kitchen, living room, and bathroom. These rooms are like namespaces in the computer world. Here's how the analogy works:

Isolation: Just as namespaces keep computer processes or programs isolated from each other, rooms in a house are separate spaces with their own purpose. You sleep in the bedroom, cook in the kitchen, relax in the living room, and use the bathroom for specific tasks. Each room is isolated from the others, like namespaces, which keep processes separate.

Resources: Each room has its own set of resources. The kitchen has cooking utensils and appliances, the bedroom has a bed, and the living room has a TV and a couch. Similarly, namespaces in computing have their own set of resources and configurations.

Interference: If you're in the kitchen, you're focused on cooking, and what happens in the living room doesn't affect you. Similarly, if a program is running in one namespace, it won't interfere with what's happening in another namespace.

Organization: Rooms help organize different activities within the house. Similarly, namespaces organize different processes or programs in the computer system, ensuring they have their own space and don't create chaos or conflicts.

<div align="center">

![image](https://i.imgur.com/6cPtjnt.gif)
</div>

--------

<div align="center">
   
## **Task 2: Learning Encoding & Encryption**
</div>

> Differentiate between encoding & encryption.

**Encryption** is a process used to convert simple readable data known as plain text to unreadable data known as ciphertext which can only be converted to plain text if the user knows the encryption key. It is used basically to keep our data safe. The main purpose of the encryption is to convert our data in such a form that it is garbage for the person who does not know the encryption key. It is used to prevent unauthorized access. The reverse of encryption is decryption and it is used to get back the plain text from the ciphertext. For decryption, we must know the encryption key and the encryption algorithm.  

**Encoding** is the use of a particular technique for changing data into a totally new format. It is a reversible process that usually involves the application of popular techniques to encode and then again decode it in its original format.

<div align="center">

![image](https://i.imgur.com/lriKrqk.png)
</div>

| Encoding                                                                                                                 | Encryption                                                                                   |
|--------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------|
| It is the process of transforming data into such a format that it can be by a different type of system using publicly available algorithms.  | It is the process to encode data securely such that only the authorized user who knows the key or password is able to retrieve the original data for everyone else it is just garbage. |
| The main purpose is the protection of the integrity of data.                                                              | The purpose of encryption is to transform data to keep it secret from others.                |
| It is used to maintain data usability.                                                                                    | It is used to maintain data confidentiality.                                                 |
| The original data can be retrieved using decoding. The algorithm used to encode the data is publicly available.         | The original data can be retrieved using decryption.                                         |
| The encryption key is not required to decrypt the data and get the original data.                                        | The encryption key is required to decrypt the data and get the original data.                |
| The encoded data is less secure. It can easily be decoded.                                                               | The encrypted data is more secure.                                                           |
| ASCII, UNICODE, URL encoding, Base64.                                                                                  | AES, RSA, and Blowfish.                                                                     |
| Viewing special characters on the web page.                                                                             | Securely sending a password over the internet.                                           |                                             |

The encrypted data is just treated like other data. We can also use more than one encryption algorithm on the same data. The real-life examples are sending someone a secret message that only they should be able to read, or securely sending a password over the Internet. The goal is data confidentiality.

Encoding has found its use in places where data cannot be transferred in its original form between applications and systems, thus keeping the data’s usability and integrity intact. However, it is not used for securing data as it is quite easy to reverse it back to its original state, so it does not take much for any attacker to decode the data in case they already have some encoded data. So obviously, encoding is not used for security purposes.

This process is used to ensure the integrity and usability of data. The real-life examples are like binary data being sent over email or viewing special characters on a web page. The main goal is data usability.

--------

<div align="center">

## **Task 3: Differentiating Tunnels & Bridges** 
</div>

> Explain tunnels & bridges in networking.

### Tunneling In Networking
Tunneling is a protocol which allows secure movement of data between devices/networks. Since there are chances of attacks when sending data through routers, we create a protection layer of tunnel. Therefore, we can undertand that tunneling involves allowing private networks communication to be sent across a public network like internet, through a secure layer called tunnel. Using Tunneling ensures confidentiality and integrity of data being transmited between networks, securely. 

<div align="center">

![image](https://i.imgur.com/IXPKNPI.png)
</div>

Some examples of Network Tunnelings along with a brief description of each are as follows:
- **Virtual Private Networks (VPN)**    
  VPNs create secure tunnels over the internet, allowing remote users or branch offices to connect to a corporate network securely. This ensures that data transmitted between the remote device and the corporate network is encrypted and protected from eavesdropping.
- **Secure Sockets Layer (SSL)**
  SSH(Secure Shell) is an access credential that is used in the SSH Protocol. In other words, it is a cryptographic network protocol that is used for transferring encrypted data over the network. It allows you to connect to a server, or multiple servers, without having to remember or enter your password for each system which is to log in remotely from one system to another. 
- **Secure Shell (SSH)** 
  SSH(Secure Shell) is an access credential that is used in the SSH Protocol. In other words, it is a cryptographic network protocol that is used for transferring encrypted data over the network. It allows you to connect to a server, or multiple servers, without having to remember or enter your password for each system which is to log in remotely from one system to another. 

### Bridges In Networking

<div align="center">

![image](https://www.rfwireless-world.com/images/network-bridge.jpg)
</div>
A network bridge is used to connect two networks together. most routers also do what bridges do. a wireless bridge, just describes the network topology the bridges works on. an ethernet bridge connects two ethernet networks together etc. say you have a wireless adapter and a ethernet adapter in your computer. you would use a bridge to connect them together. One of the best examples of when bridge networks can be used is between Host system and Virtual Machines

--------

<div align="center">
   
## **Task 4: Understanding System Booting**

</div>

> Explain how a system boots or starts.

The Linux boot process is a series of steps that occur when a computer running a Linux operating system is powered on or restarted. It involves several stages to initialize the hardware, load the kernel, and bring the system to a usable state. A visual representation of the processes involved is as follows:

<div align="center">

![image](https://www.freecodecamp.org/news/content/images/2020/03/LinuxBootingProcess.jpg)
</div>

In more detail, the overview of the Linux boot process is as follows:

- **BIOS - Basic I/0 system**
  -  First Program that executed which is stored in read-only memory on motherboard of computer.
  - Perform POST (power-on self-test) verify the hardware components and peripheral to ensure if computer is in working condition.
  - Check for bootable device like pendrive, hardisk etc.
  - Handover control to first sector of device i.e. MBR
Apart from BIOS, UEFI (Unified Extensible Firmware Interface) is used.

- **MBR - Master Boot Record**
  - 512 bytes, first sector of any bootable device contains machine code instructions to boot a machine and having following information:     
    - Boot loader (446 bytes)   
    - Partition Table (64 bytes)    
    - Error Checking (2 bytes)    
  - It will load the boot loader into the memory and handover to it.
  - Load /boot/grub2/grub.cfg at boot time
  - At this stage, User will see GUI asking different OS or kernels configured to boot.
  - Once we select the kernel, it locates the corresponding kernel binary

- **​GRUB - Grand Unified Bootloader**
  - /boot/vmlinuz-`kernel-version`
  - Main job is to load kernel and initrd/initramfs image into memory
  - Once load kernel in RAM, it passes control to it
  - ​In most Linux distributions, the default boot loader is GRUB2

- **Kernel**
  - Kernel will load in Read-Only mode.  
  - Even by now, system is booting up since the main file system has not loaded yet. 
  - Initramfs/Initrd will get decompressed & then temporary file system will be loaded, for loading the actual file system
  - Once the main system file has bee mounted, the kernel initialises its first process called systemd, where d stands for daemon or a process that runs in background
  - Systemd (earlier known as init) is first process with Process ID 1 and starts all the required processes.

- **Target**
  - Targets are a specific runlevel/system-state that the operating system is set to achieve during the boot process
  - Targets help define the state in which a Linux system should be when it starts up
  - The running target can be viewed by running the `systemctl get-default` command
  
_____________________________


<div align="center">
   
## **Task 5: Modifying Podman's Data Directory**

</div>

> For Podman, Create a directory `/data` & change the default data directory for containers from the default directory of `/var/lib/containers`.

As per the assigned task, we were supposed to created a brand new directory for `/data`. In order to perform this task, I utilised [this document](https://docs.oracle.com/en/operating-systems/oracle-linux/podman/podman-ConfiguringStorageforPodman.html#configuring-podman-storage) by Oracle. Since it was mentioned in the mail that this directory was to be created under the root system, I ran `sudo mkdir /data` to create a directory under the root hierarchy. A go-through of how this task was done is as follows:
<div align="center">

![image](https://i.imgur.com/dyoCNd2.gif)
</div>

Given Podman's default data directory is `/var/lib/containers` and that I needed to change it to `/data` directory instead, I opened the `storage.conf` file that was located inside the `/etc/containers` directory. Under the 'Primary Read/Write location of container storage' section of this configuration file, In addition to the above go-through, I also uncommented the `rootless_storage_path` and set it as `/data`.

I replaced the original path of data storage fo containers with the `/data` directory. I ran `sudo systemctl restart podman` to update the recent changes made to the configurations of Podman. Finally, in order to ensure that this change had indeed taken place, 

I ran the `podman info` command to view the data directory for podman containers. The output of this command showed that the change in the data directories had not taken place:
<div align="center">

![image](https://i.imgur.com/4hcu493.png)
</div>

Therefore, I was able to successfuly change the default container data storage path from `/var/lib/containers` to `/data` using the steps that have been mentioned above.
_____________________________

## **Task 6: Performing DO188 Guided Excercises**

</div>

As per this task, the participants were expected to 

## **Task 6.1: Chapter 2 Guided Exercises**
## **Task 6.1.1: Creating Containers with Podman**
> Create several Podman containers by using different options.


## **Task 6.1.2: Accessing Containerized Network Services**
> Run two applications that communicate by using the Podman DNS system.

## **Task 6.1.3: Accessing Containers**
> Use the podman exec and podman cp commands to debug and correct container configuration.

## **Task 6.1.4: Managing the Container Lifecycle**
> Manage the lifecycle of a container that runs an Apache HTTP server.


<div align="center">

![image](https://i.imgur.com/6cPtjnt.gif)
</div>

_____________________________


  <div align="center">

## **Conclusion**
</div>

Through this 

--------

