<div align="center">


<!-- add technical charcha logo postgres session 3 -->
# Kubernetes Assignment 1        
### — A Task Documentation by Yash Anand —    

_____________________________________________________________________________________                        

## Contents
</div>


- [Overview](#overview)
- [Prerequisites](#prerequisites)
- [Task 1: Understanding Namespaces](#task-1-understanding-namespaces)
- [Task 2: Learning Encoding & Encryption](#task-2-learning-encoding--encryption)
- [Task 3: Differentiating Tunnels & Bridges](#task-3-differentiating-tunnels--bridges)
  - [Tunneling In Networking](#tunneling-in-networking)
  - [Bridges In Networking](#bridges-in-networking)
- [Task 4: Understanding System Booting](#task-4-understanding-system-booting)
- [Task 5: Modifying Podman's Data Directory](#task-5-modifying-podmans-data-directory)
- [Task 6: Performing DO188 Guided Exercises](#task-6-performing-do188-guided-exercises)
  - [Chapter 2](#chapter-2)
  - [Chapter 3](#chapter-3)
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

## **Task 1: Understanding Namespaces**
</div>

> Explain namespaces, their types & uses.   

Namespaces can be understood as enclosures that provide process and resuorce isolation. They allow different processes or containers to have their own view of various system resources, making it possible to run multiple instances of a resource without them interfering with each other. Linux namespaces are primarily used in containerissation technologies like Docker and Kubernetes. Here are some examples of types of namespaces in Linux:

**PID Namespace**:    
ProcessID namespaces isolate the process IDs of a group of processes. Each namespace has its own set of process IDs, ensuring that processes in one namespace can't see or interfere with processes in another.

**Mount Namespace**: 
Mount namespaces provide an isolated view of the filesystem. Each namespace has its own mount points, so processes within a namespace can have a different view of the filesystem, even if they are running on the same physical machine.

**Network Namespace**: 
Network namespaces isolate network resources such as network interfaces, routing tables, and firewall rules. This allows each namespace to have its own network stack, making it possible to create separate network environments for different containers or processes.

**User Namespace**:  
User namespaces map user and group IDs inside a namespace to different IDs outside the namespace. This is crucial for security and allows a container, for example, to have its own user and group IDs while remaining isolated from the host system.

**Cgroup Namespace**:  
Cgroup namespaces provide isolation for control groups (cgroups), which are used for resource management and limiting resource usage by processes.


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

<div align="center">

## **Task 6: Performing DO188 Guided Excercises**
</div>

As per this task, the participants were expected to utilise the Guided exercises from the Red Hat DO-188 Course's chapters provided below:
-  Chapter 2: Podman Basics
-  Chapter 3: Container Images

In this section, I will be covering all the Guided Exercises from the chapters mentioned above.

<div align="center">

## **Chapter-2**
</div>

> Creating Containers with Podman

<div align="center">

## **6.1. Creating Containers With Podman**
</div>

## **6.1.1: Creating Containers with Podman**
> Create several Podman containers by using different options.

In order to create a container using the RedHat Lab after I had logged into the `workstation machine` and had signed into it as the `student` user, it was required for me to first prepare my system for this exercise. Therefore, I first ran he `lab start basics-creating` command and once that had been done, I first ran the command provided below:
```
podman pull \
 registry.ocp4.example.com:8443/ubi8/ubi-minimal:8.5
```
Output:
<div align="center">

![image](https://i.imgur.com/wSOyl9X.png)
</div>

The use of the above command was to fetch the image from the registry for creating a container. Once I had fetched the image, it was important to ensure that it had truly been fetched and in order to do so, I ran the following command:
```
podman images
```  
Output:
<div align="center">

![image](https://i.imgur.com/pUekq5b.png)
</div>

The output of the above command successfuly showed that the image that we had fetched had truly been pulled. Given that I had the access to the container image, it was now possible to create a container out of it while also making sure that the command had run. In order to do so, I ran the following command:
```
podman run --rm \
 registry.ocp4.example.com:8443/ubi8/ubi-minimal:8.5 echo 'Hello Red Hat'
```  
Output:
<div align="center">

![image](https://i.imgur.com/VzmZCCH.png)
</div>

The displayed output of the above command verified that the command had been executed since the message added for echoing in the terminal had certainly been echoed. Since I had not started the container yet, it was only expected for it be not running after the execution of the `podman run` command had been done. To ensure this was the case, I ran the following command:
```
podman ps
```  
Output:
<div align="center">

![image](https://i.imgur.com/DPoqu71.png)
</div>

In the above output, I was unable to view the container that I had just created listed in the output. Therefore, we could now move to the next section.

## **Task 6.1.2: Accessing Containerized Network Services**
> Run two applications that communicate by using the Podman DNS system.

As per the sub-task of creating a container in Podman, I was expected to set and understand the basics of the environment variables of the container image that I had pulled previously. In order to do so, I used the command provided below for setting the environemnt variables of the container that was to be again created. It should be noted that I used the `-e` flag for setting the environment variables:
```
podman run --rm -e GREET=Hello -e NAME='Red Hat' \
 registry.ocp4.example.com:8443/ubi8/ubi-minimal:8.5 printenv GREET NAME
```
Output:
<div align="center">

![image](https://i.imgur.com/u6YaujQ.png)
</div>

Given that the environment variables had been printed as the output, it meant that the variables had been set sucessfuly. Again since I had not started the container, it was expect that the container would not be shown as running if the following command was run
```
podman ps
```
Output:
<div align="center">

![image](https://i.imgur.com/DPoqu71.png)
</div>

## **Task 6.1.3: Accessing Containers**
> Use the podman exec and podman cp commands to debug and correct container configuration.

Now that I had understood how environment variables were set, I created a new container for `httpd-24`. In order to do so, I directly ran the `podman run` command before downloading its container image first. The container was set to listen on port 8080 of container and machine. The entire command for creating such a container was as follows:
```
podman run --rm -p 8080:8080 \
 registry.ocp4.example.com:8443/ubi8/httpd-24

```
Output:
<div align="center">

![image](https://i.imgur.com/q8SB47A.png)
</div>

In order to ensure that the container had started and that its `httpd` services were working as expected, I opened up my browser and searched the following URL on my Red Hat Workstation Lab's Firefox:
```
localhost:8080
```
Output:
<div align="center">

![image](https://i.imgur.com/1kcy9vM.png)
</div>

The above output successfuly showed that the HTTPD service had started working on the system after creating the `httpd container`. However, in order to ensure that this container could be allowed to run in the background without having to risk the stopping of the container in case of terminal's exit, I pressed `CTRL+C` and ran the following command for running the command in detatched mode:
```
podman run --rm -d \
-p 8080:8080 registry.ocp4.example.com:8443/ubi8/httpd-24
```
Output:
<div align="center">

![image](https://i.imgur.com/M1km4VR.png)
</div>

Running `podman ps` after creating the detached container using the `-d` flag, I was able to successfuly verify that the container had certainly been created and was indeed working in the background. Given that this Guide Exercise had been completed, I could now move on to the next Guide Exercise from the Chapter once again but before that, I ran the `lab finish basics-creating` command to ensure that the experiments done in this section would not affect the future experiments:
<div align="center">

![image](https://i.imgur.com/Pux4Qi1.png)
</div>
_____________________________

<div align="center">

## **6.2. Accessing Containerized Network Services**
</div>

As per the second Guided Exercise from the Chapter-2, we were supposed to run two applications that would be able to communicate with eachother using the Podman DNS System. The objective of this exercise was to help us better understand the workings of DNS in Podman Networks.The two applications were `times` and `cities` and it was expected they would communicate.

Before I could get started with the exercises, I ran the following command for starting a lab environment with some basic network services:
```
lab start basics-exposing
```
Output:
<div align="center">

![image](https://i.imgur.com/FJ9QcIX.png)
</div>

## **6.2.1: Application Source Codes**
> Examine the source code of the applications.

The first exercise was to look into the source codes of the two applications and in order to do so, it was required to enter the directory in which these applciations were located in. This was done by running the following command:
```
cd ~/DO188/labs/basics-exposing
```
Output:
<div align="center">

![image](https://i.imgur.com/10mogcU.png)
</div>

```
cat podman-info-times/app/main.go
```
Output:
<div align="center">

![image](https://i.imgur.com/yGVvyAE.png)
</div>

```
cat podman-info-cities/app/main.go
```
Output:
<div align="center">

![image](https://i.imgur.com/aAWEVWs.png)
</div>

Lastly, I ran the `cd ~` command for returning back to the home directory since I had verified and learnt about the ports of both the applications that were being used by the applications.

## **6.2.2: Podman Network With DNS**
> Create a Podman network with DNS enabled

```
podman network inspect podman
```
Output:
<div align="center">

![image](https://i.imgur.com/tmvZ48B.png)
</div>

```
podman network create cities
```
Output:
<div align="center">

![image](https://i.imgur.com/ZPCOQCr.png)
</div>

```
podman network inspect cities
```
Output:
<div align="center">

![image](https://i.imgur.com/bFZGvFG.png)
</div>

## **6.2.3: Testing Networked Applications**
> Start and test the times application attached to the cities network.

```
podman run --name times-app \
--network cities -p 8080:8080 -d \
registry.ocp4.example.com:8443/redhattraining/podman-info-times:v0.1
```
Output:
<div align="center">

![image](https://i.imgur.com/XyOC9Hx.png)
</div>

```
podman inspect times-app \
-f '{{.NetworkSettings.Networks.cities.IPAddress}}'
```
Output:
<div align="center">

![image](https://i.imgur.com/ZZNMYHT.png)
</div>

```
podman run --rm --network cities \
registry.ocp4.example.com:8443/ubi8/ubi-minimal:8.5 \
curl -s http://10.89.0.2:8080/times/BKK && echo
```
Output:
<div align="center">

![image](https://i.imgur.com/mosOqDN.png)
</div>

```
podman run --rm --network cities \
registry.ocp4.example.com:8443/ubi8/ubi-minimal:8.5 \
curl -s http://times-app:8080/times/BKK && echo
```
Output:
<div align="center">

![image](https://i.imgur.com/Ci9HQVn.png)
</div>

## **6.2.4: Starting Networked Applications**
> Start and test the cities application attached to the cities network.

```
podman run --name cities-app \
--network cities -p 8090:8090 -d \
-e TIMES_APP_URL=http://times-app:8080/times \
registry.ocp4.example.com:8443/redhattraining/podman-info-cities:v0.1
```
Output:
<div align="center">

![image](https://i.imgur.com/xXJD3Uz.png)
</div>

```
curl -s http://localhost:8090/cities/MAD | jq
```
Output:
<div align="center">

![image](https://i.imgur.com/1Qq0TE5.png)
</div>

```
curl -s http://localhost:8090/cities/SAN | jq
```
Output:
<div align="center">

![image](https://i.imgur.com/1Qq0TE5.png)
</div>

Given that I had been able to successfuly run two applications while using the containerised network services. therefore it was time to finish this exercise on the Workstation by running the command of `lab finish basics-exposing`
____________________________

<div align="center">

## **6.3. Accessing Containers**
</div>

> Use the podman exec and podman cp commands to debug and correct container configuration.

The objective of this exercise was to help me better understand the `podman exec` and `podman cp` commands for debugging and correcting container configurations. The idea was to be able to execute commands inside of a container and also for copying files form and into a container

Before I could get started with the exercises, I ran the following command for starting a lab environment:
```
lab start basics-accessing
```
Output:
<div align="center">

![image](https://i.imgur.com/R9dImbX.png)
</div>

## **6.3.1: Create New Containers**
> Create a new container with the following parameters:     
> Container name: nginx   
> Container image: registry.ocp4.example.com:8443/redhattraining/podman-nginx-helloworld  
> Route traffic from port 8080 on your machine to port 8080 inside of the container. Use the -d option to run the container in the background.    

```
podman run --name nginx -d -p 8080:8080 \
  registry.ocp4.example.com:8443/redhattraining/podman-nginx-helloworld
```
Output:
<div align="center">

![image](https://i.imgur.com/rBjzST9.png)
</div>

## **6.3.2: Browsing Nginx**

The next step was to navigate to `localhost:8080` in order to find the `404 Not Found` error, which I did by opening this URL in the Firefox browser.   
Output:
<div align="center">

![image](https://i.imgur.com/6jq7bfU.png)
</div>

## **6.3.3: Troubleshoot The Issue**

In order to troubleshoot this `404 Not Found` Error, I ran the `podman cp nginx:/var/log/nginx/error.log error.log` command for copying the nginx logs to my system. Once I had done so, I opened the `error.log` in gedit for finding what the issue was using the following command:
```
gedit error.log
```
Output:
<div align="center">

![image](https://i.imgur.com/94i2T5z.png)
</div>
Inside this log file, I was able to find that the `/usr/share/nginx/html/public/index.html` file was not being read. In order to ensure that this directory did indeeed exist, I tried to access it using the `podman exec nginx ls /usr/share/nginx/html/public` but I was unable to do so due to `ls: cannot access '/usr/share/nginx/html/public': No such file or directory`. This meant that the directory did not exist inside the container.

Since the `public` sub-directory did not exist, I further verfieid the existence of `/usr/share/nginx/html` to know if atleast it was in existence using the following command:
 ```
podman exec nginx ls /usr/share/nginx/html
```
Output:
<div align="center">

![image](https://i.imgur.com/sdLcXMz.png)
</div>

## **6.3.4: Correct the server configuration**

Through the above output, I was able to verify the existence of index.html and in order to correct the server configurations, I copied the `nginx.conf` file from the container to my machine using the `podman cp nginx:/etc/nginx/nginx.conf .` command and then opened up this configuration file on my system using the `gedit nginx.conf` command. 

In the configuration file, I was supposed to replace the root path to `/usr/share/nginx/html/` but in my case, this was already set as the path. To correct the configuration file, I added the following lines:
```
listen       8080 default_server;
server_name  _;
root         /usr/share/nginx/html/;
``` 

Afterwards, I ran the `podman cp nginx.conf nginx:/etc/nginx` command for replacing `/etc/nginx/nginx.conf` with the modified nginx.file from my system.
<div align="center">

![image](https://i.imgur.com/9UXe978.png)
</div>

## **6.3.5: Verfiying Functionality Of Container**

To ensure that the container would be able to run after the changes made, I first restarted it using the `podman exec nginx nginx -s reload` command and then opened up `localhost:8080` on the Red Hat Workstation Machine's Firefox browser:

After the changes, made I was able to run make the `Hello world from nginx!` message displayed as the output of `localhost:8080`:
<div align="center">

![image](https://i.imgur.com/XVtyvem.png)
</div>

Additionally, since this exercise had been completed, I decided to run the the `lab finish basics-accessing` command for finishing the lab environemnt that had been ceated so far.
__________________________

<div align="center">

## **6.4. Managing Container Lifecycle**
</div>

> Manage the lifecycle of a container that runs an Apache HTTP server.

As per this exercise, it was expected that we would be able to gain ideas about the following Podman concepts:
- Get detailed information about a container.
- Stop containers.
- Restart a stopped container.
- Delete containers.

Similar to the previous exercises, in order to get started woth this exercise, it was requried to first ensure that `lab start basics-lifecycle` command had been run for creating a safe environment. 

<div align="center">

## **6.4.1: Creating Container With Apache Server**
>  Create a container that runs an Apache HTTP server in the background.
</div>

```
podman run --name httpd -d -p \
 8080:8080 registry.ocp4.example.com:8443/ubi8/httpd-24
```
Output:
<div align="center">

![image](https://i.imgur.com/TVCXSw1.png)
</div>

## **6.4.2: Verify Container Is Running**

In order to ensure that the container that was just created in the previous step, I needed to run the `podman ps` command for ensuring that the container had truly been created. However, there were some other way of checking whether the container was running or not, such as `podman inspect --format='{{.State.Status}}' httpd` as well as the `podman inspect --format='{{.State.Running}}' httpd` commands.

The outputs of these commands were as follows:
Output:
<div align="center">

![image](https://i.imgur.com/q1hVcvc.png)
</div>

Additionally, I also ran `locahost:8080` in a web browser and I was able to see that the Apache Server was running. Therefore, through these 4 methods, I was able to confirm that my container was up and running.

## **6.4.3: Stop The Container**

In this section, the objective for this task was to stop the running container that had been started previously. Therefore, in order to stop a running container, I ran the `podman stop httpd` command. In order to ensure that this container had truly been stopped, I ran the `podman inspect --format='{{.State.Status}}' httpd` and `podman inspect --format='{{.State.Running}}' httpd` commands. The output of running these was as follows:
<div align="center">

![image](https://i.imgur.com/DlLiU43.png)
</div>

To further ensure that the container had stopped, I also opened my the Firefox web browser on the Red Hat Workstation Lab and ran `localhost:8080` on it to see if it was no longer accessible, which it was not.

## **6.4.4: Restart The Container**

Given that the container had been just stopped in the previous section, in this section I worked on restarting it. In order to restart it, I ran the `podman restart httpd` command and then `podman ps` for ensuring that the container had been restarted. The output of running both of these commands was as follows: 

<div align="center">

![image](https://i.imgur.com/e7atUML.png)
</div>

To check if the httpd service was available on `localhost:8080`, I opened up the URL in the Firefox web browser. The output of doing so was that the service was indeed up and running.

## **6.4.5: Removing The Container**

The usual method of removing a container is by running the `podman rm <container>` or `podman rm httpd` command. However, when I ran this command, I was shown an error stating that this container was already up and running since I had restarted it earlier. In order to remove it anyway without having to stop the container, I ran the `podman rm httpd --force` command which allowed me to successfuly remove the running container. The output of these commands was as follows:
<div align="center">

![image](https://i.imgur.com/tq7kFfQ.png)
</div>

## **6.4.6: Verifying Removal Of Container**
In order to ensure that the container removed in the previous section had been truly removed, I ran the `podman inspect --format='{{.State.Running}}' httpd` command. Since the container had really been removed, I was able to successfuly get the following output which signified the removal of the container:
<div align="center">

![image](https://i.imgur.com/B2Tfhuj.png)
</div>

## **6.4.7: Forcefully Stopping Container If SIGTERM Fails**
> Forcefully stop a container that does not respond to the SIGTERM signal.

SIGTERM 15 is a linux process that carries out the termination of processes. In this section, I will be stopping an application in which SIGTERM fails to kill or terminate a container running in podman. In order to do so, I first created a container of an application which by default ignroes `SIGTERM 15` signal. For creating such a container, I first ran the following command for creating the greeter container.
```
podman run --name greeter -d \
registry.ocp4.example.com:8443/redhattraining/podman-greeter-ignore-sigterm
``` 
Output:
<div align="center">

![image](https://i.imgur.com/CPqCb6I.png)
</div>

Once the container had been created using this method, I ran the `podman stop greeter --time=5` command which in turn gave the output of `WARN[0005] StopSignal SIGTERM failed to stop container greeter in 5 seconds, resorting to SIGKILL`. What this output means is that Podman will try to wait for 5 seconds until an application has been stopped and it isn't stopped, Podman will send the `SIGKILL` process for forecully killing the container.

For directly sending the `SIGKILL` process, I also restarted the container using the `podman restart greeter` command and ran the `podman kill greeter` command for directly sending the `SIGKILL` process to kill a container. The output of doing so was as follows:
Output:
<div align="center">

![image](https://i.imgur.com/oA5K7JW.png)
</div>

Given that this exercise had been completed, I finally ran the `lab finish basics-lifecycle` command for putting the lab created for this exercise back to sleep.
________________________

<div align="center">

## **Chapter-3**
</div>

<div align="center">

## **1. Container Image Registries**
</div>

As per this Guided exercise, the goal is to gain a better understanding of logging in to container image registries, moving container images between registries and testing quay images. In order to et started with this exercise, I first ran `lab start images-basics`.

## **1.1 Login To RHOCP**

As per the first sub-task, it was required for me to lgoin as the admin to the RHOCP using the following command:
```
oc login -u admin -p redhatocp \
    https://api.ocp4.example.com:6443
``` 
Output:
<div align="center">

![image](https://i.imgur.com/RZsO4Va.png)
</div>

As per the output above, I was able to successfuly login to the RHOCP. Having logged in to the RHOCP, it was now necessary for me to login to the RHOCP registry using Podman. This particular sub-task was executed by running the following command:
```
podman login -u $(oc whoami) -p $(oc whoami -t) \
  default-route-openshift-image-registry.apps.ocp4.example.com
``` 
The output of the above command was `Login Succeeeded!` and having logged into RHOCP Registry, it was also possible for me now to login into the `registry.ocp4.example.com:8443` using Podman. Like the previous commands, the output of this commad was also successful as I was shown `Login Succeeded!` for the following command:
```
podman login -u developer -p developer \
  registry.ocp4.example.com:8443
``` 
The output of all the commands mentioned above was as follows:
<div align="center">

![image](https://i.imgur.com/D82Fsr5.png)
</div>

Given that the logging in to RHCOP had been completed, I could now copy the container image using a tool called skopeo, which is used for manipulating container images.

## **1.2 Copying Container Image**
> Use skopeo to copy the default-route-openshift-image-registry.apps.ocp4.example.com/default/python:3.9-ubi8 image to the registry.ocp4.example.com:8443 registry.

Here I have copied a container image from one registry to another. tHE copying of the image is happening from the Docker registry to the RHOCP registry. This was using the following commands:
```
\
RHOCP_REGISTRY="default-route-openshift-image-registry.apps.ocp4.example.com"
skopeo copy --dest-tls-verify=false \
docker://${RHOCP_REGISTRY}/default/python:3.9-ubi8 \
docker://registry.ocp4.example.com:8443/developer/python:3.9-ubi8
```
Output:
<div align="center">

![image](https://i.imgur.com/T4IvjhS.png)
</div>

## **1.3 Making Image Public**

Despite the image container not being able to copied, I decided to look into how in the internal registry, an image could be made public. To do so, I opened `https://registry.ocp4.example.com:8443` in my Red Hat Workstation. Once the website had been opened, I logged into it using `developer` as password and username:
<div align="center">

![image](https://i.imgur.com/c3aiqPM.png)
</div>

Once I had logged into the site, I searched for `developer` in the Filter repository field and clicked `developer/python` repository. However, the result was "No Matching Repositories", which was unlike what was supposed to happen as per the task.

## **1.4 Testing Image As Unauthenticated User**
> Test the image as an unauthenticated user.

In order to see the output of how a container would get created as an unauthenticated user, I ran the `podman logout --all` command for logging out of all the registries. Now to check what the output would have been if I tried to pull the registry.ocp4.example.com:8443/developer/python:3.9-ubi8 image, I ran the following command:
```
podman pull \
  registry.ocp4.example.com:8443/developer/python:3.9-ubi8
podman run --rm \
  registry.ocp4.example.com:8443/developer/python:3.9-ubi8 python3 --version
```
Since the above image had not been made public in the previous section, I was displayed the `Unauthorised` error. In order to start the image that was supposed to be pulled in the output provided above, the second command was ran by me to start the container but since the image had not been pulled due to not being public, I was unable to carry out this task.

Output:
<div align="center">
![image](https://i.imgur.com/a2PMoPK.png)
</div>

In order to finish this lab session on my Red Hat workstation, I ran the command of `lab finish images-basics`.

______________

## **2. Managing Images**
>Learn to manage container images

The objective of this particular Guide exercise was to help me to peform the following actions:
- Creating images
- Listing images
- Inspecting images
- Tagging images
- Removing images
- Searching images
- Pulling images

In order to prepare the system for this exercise, I ran the `lab start images-managing` command for creating a copy of ContainerFile that is used for building simple-server image. 

------------------------------------

