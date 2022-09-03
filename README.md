# Poridhi DevOps Documentation
## _Classes_
##### Class 1 (Basic Networking)
- OS Space & NIC
- IP Address
- Subnet and Subnet Mask
- NAT (Network Address Translation)
- CIDR (Classless Inter Domain Routing)
- Hub
- DHCP (Border Gateway Protocal)
- Switch
- Router
- AS (Autonomus System)
- BGP (Border Gateway Protocal)
##### Class 2 (Cloud Networking)
- OSI Layers
- Tansport Layer
- Payload
- Socket Binding
- Three Way Hand Shaking
- Cloud NAT
- WebSockets
- Physical Machine
- Virtual Machine
- Container
##### Class 3 (Google Cloud Basic)
- Aim & Workflow
- VPC Network
- Virtual Machine
- Firewall
- NGINX
- Check Status
##### Class 4 (GCP and Docker Networking with Monitoring)
- Aim & Workflow
- IP monitoring from VM
- IP monitoring from Container 

## _Class 1 (Basic Networking)_
### _Topics: OS Space, NIC, IP Address, Subnet, CIDR, Hub, DHCP, Switch, Router, AS, BGP_
- **OS Space & NIC:** VM (Virtual Machine) has two spaces. One _User Space_ and another _Kernel Space_. _User Space_ contains applications which communicate with _Network stack_. Communication is done through data packet. _Network stack_ sends the data packet to _NIC (Network Interface Controller)_ and this NIC send that outside. Follow the example below:-

![N|NIC](https://drive.google.com/uc?export=view&id=1QYyFaLwPO8yW4dVeB37xsCNRhP1WHg4L)

- **IP Address:** IP Address has four blocks. We call each block as _octate_. Each block has 8 bits. Number range foreach block is between (0 - 255). In total IP address consume 32 bits (4 * 8 bits). IP Address has two parts. _Host part_ and _Network part_. _(Note: To allocate all users IP addresses we need NAT. Later we will discuss about it)_. Now, IP Address has two range. _Public Range_ and _Private Range_. This public range has been splited into different region. We call it as _Subnet_.To represent subnet first Class A, Class B, Class C, ... notations were used. But later a very popular notation were introuced and that is _CIDR (Classless inter domain routing)_.

- **Subnet and Subnet Mask:** A network connecting the host interfaces and one router interface having the same IP address format is called _Subnet_. It is represented as a.b.c.d/x where _/x_ is called as Subnet Mask. 

- **NAT (Network Address Translation):** Network Address Translation or NAT is a process where it converts Private IP Address to Public and Public to Private. Through this private IP Addresses can communicate with public IP Address. To maintain conversion NAT uses _NAT Translation Table_ where it maps Private and Public IP Addresses. 

- **CIDR (Classless Inter Domain Routing):** CIDR notation looks something like this _12.13.0.0/16_. CIDR notation has two parts. One _Network_ and other _Host_. Now, here _12.13_ is the _Network_ part and _0.0_ is the _Host_ part. Also, 16 represents occupied bits by the _Network_ part. So, under a network 2^16 - 2 host addresses can be provided.

## _Layer 2 (Data) Devices:_
- **Hub:** Hub is a network connection among devices. In past we need to manually define IP addresses foreach machine that are conected to that _Hub_. For this, we need to maintain a table by hand. If not then that will increase the change of over lapping IP addresses.

![N|NIC](https://drive.google.com/uc?export=view&id=12gYY_KAKeAFJNe3TGc_lyJwuZgAOZc1_)

- **DHCP:** In order to overcome this manual situation DHCP is being introduced. DHCP contains a HashMap (MAC, IP Address). This thing dynamically provide IP Address to a MAC. See the example below. Note: If we ping under same network then data packet will not go out of NIC card of the switch.

- **Switch:** Switch is an ungrade version of _Hub_. Its being used for inter device communication. It maintains a _MAC_ table. Now, If we ping 12.13.0.3 from Device 1  then this request will request DHCP for the MAC. Then we get BBB MAC address. Now, switch will try to find the MAC in MAC table and its related port information. After that the connection is being established.

![N|NIC](https://drive.google.com/uc?export=view&id=1Rp-Oq_87PdOGpSKT3HjxiSs8ojbah59T)

## _Layer 3 (Network) Devices:_
- **Router:** Router is being used for inter network communication. Now if we ping outside the network then what will happen? See the example below. As D1 ping 10.15.0.2 which is not under S1 switch then the data pack will go out of the gateway to router. Then it will try to find 10.15.0.0 under the table which is RI2 interface. Then the data pack will go to S2 switch to D2 device. By this way the connection is being established.

![N|NIC](https://drive.google.com/uc?export=view&id=1WGJFtDD5vQi2jY3buDOjoJcyHG6gUJdx)

- **AS:** AS stands for Autonomus System. It connects tousands of routers of  ISP (Internet Service Provider). AS handle internet connections of a region. Many region AS are conected together to bring the world under a common network which we called internet. AS has two parts, IBGP (Inter Border Gateway Protocal) and EBGP (External Border Gateway Protocal)

- **BGP:** BGP stands for Border Gateway Protocal. BGP make sure data packet can be send/receive from one region to another effectively. For this it needs to maintain a table which helps a data packet to travel a shortest part to reach its destination. Time to time it gets it self updated.

## _Class 2 (Cloud Networking)_
### _Topics: OSI Layers, Tansport Layer, Payload, Socket Binding, Three Way Hand Shaking, Cloud NAT, WebSockets, Physical Machine, Virtual Machine, Container_
- **OSI Layers:** OSI stands for  _Open Systems Interconnection_. The layers can be memorized by _APSTNDP_. Layer description is given below.

| Short Form | Elaboration | Layer |
|------------|-------------|-------|
| A | Application | L7 |
| P | Presentation | L6 |
| S | Session | L5 |
| T | Transport | L4 |
| N | Network | L3 |
| D | Data Link | L2 |
| P | Physical | L1 |

## _Layer 4 (Transport):_
- **Transport Layer:** Transport Layer is the second layer in the TCP/IP model and the fourth layer in the OSI model. It is an end-to-end layer used to deliver messages to a host. It is termed an end-to-end layer because it provides a point-to-point connection rather than hop-to- hop, between the source host and destination host to deliver the services reliably. The unit of data encapsulation in the Transport Layer is a segment. For more info follow [GeeksForGeeks](https://www.geeksforgeeks.org/transport-layer-responsibilities/)

- **Payload:** Payload consists of four segments. _SIP (Source IP), SP (Source Port), DIP (Destiation Port), DP (Destination Port)_

- **Socket Binding:** Binding a port with a _Kernel Space_ socket is called _Socket Binding_. For more infor follow [Youtube](https://www.youtube.com/watch?v=059EKGJWilU&ab_channel=GateSmashers)

- **Three Way Hand Shaking:** To understand _Three Way Hand Shaking_ follow [this](https://www.youtube.com/watch?v=qIEHUUt2Wfc&ab_channel=GateSmashers) youtube video.

- **Cloud NAT:** Google cloud virtual machines need to communicate through internet by using Clound NAT. Its follows (I can access you but you can't access me if I don't allow). Follow [this](https://www.youtube.com/watch?v=qIEHUUt2Wfc&ab_channel=GateSmashers) youtube video for more details.

- **WebSockets:** GThe WebSocket API is an advanced technology that makes it possible to open a two-way interactive communication session between the user's browser and a server. With this API, you can send messages to a server and receive event-driven responses without having to poll the server for a reply. For more details go to [this](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API) link.

- **Physical Machine:** Physical Machine is a collection of CPU, RAM, Hard Disk hardwares upon which an operating system operates on which installed application runs.

- **Virtual Machine:** A virtual machine (VM) is a virtual environment that works like a computer within a computer. It runs on an isolated partition of its host computer with its own CPU power, memory, operating system (such as Windows, Linux, macOS), and other resources. End users can run applications on VMs and use them as they normally would on their workstation.

- **Container:** Container is an application packet which contains the application, its dependencies and linux basic system. It operates on hosted machine OS Kernel. Through dynamic allocation of system physical resources it speed up performance.  

## _Class 3 (Google Cloud Basic)_
### _Topics: Aim & Workflow, VPC Network, Virtual Machine, Firewall & NGINX_
- **Aim & Workflow:** In-order to deploy a developed system on google cloud we need to configure VPC Network, Virtual Machine (VM) and Firewall. The aim of this class is to configure these and check final configured system status. To achieve follow this workflow: 
    1. Create VPC Network
    2. Create Virtual Machine
    3. Firewall
    4. Setup nginx server
    5. Check Status

- **VPC Network:** After login in google cloud on serch box write _VPC Networks_ and choose it. While creating network provide 
    - Name, 
    - VPC network ULA internal IPv6 range (Disabled),
    - Subnet
        * Name
        * Region (us-east-1)
        * IP stack type (IPv4 (single-stack))
        * IPv4 range (10.10.0.0/16)
        * Private Google Access (off)
        * Flow logs (off)
    - Firewall rules (As it is)
    - Dynamic routing mode (Regional)
    - Maximum transmission unit (MTU) (1460)

- **Virtual Machine:** On serch box write _VM Instances_ and choose it. While creating instance provide 
    - Name, 
    - Region (us-east-1)
    - Zone (us-east1-b)
    - Machine configuration (Under GENERAL-PURPOSE)
        * Series (E2)
        * Machine Type (e2-medium)
        * Boot Disk (Size 20 GB) {_Note: You can change operating system here_}
    - Advanced Options
        * Network -> Network interfaces -> (Choose created VPC network name)

- **Firewall (To access VM from SSh):** To access VM through SSH we need to allow IAP (Identity Aware Proxy) using Firewall. While this creating firewall provide 
   - Name, 
   - Logs (off),
   - Priority (1000)
   - Direction of traffic (Ingress)
   - Action on match (Allow)
   - Targets (All instances in the network)
   - Source IP Range (35.235.240.0/20)
   - Protocols and ports (TCP: 22)

- **Firewall (To access VM hosted website):** To access VM hosted website we need to allow all IP using Firewall. While this creating firewall provide 
   - Name, 
   - Logs (off),
   - Network (Choose created VPC)
   - Priority (1100)
   - Direction of traffic (Ingress)
   - Action on match (Allow)
   - Targets (All instances in the network)
   - Source IP Range (0.0.0.0/0)
   - Protocols and ports (Allow all)

_Note:_ After creating these firewalls check VM _External IP_ access using cmd ping. Need to keep in mind that by providing _Allow all_ for _Protocal and ports_ is a bad practice. Providing a specific protocol and port makes it secure. For this reason we will provide the follow _(tcp:80, icmp)_. Here, tcp:80 will allow browsing the server and icmp will allow pinging the IP address. Also check SSH to access VM.

- **NGINX:** Now we need to setup _nginx_ and test the trafiq. Go to created VM and click SSH. When VM opens then follow these steps:
   - sudo apt update, 
   - sudo apt install nginx
   - Now copy the external ip and check _tracert {ip address}_
   - Also, go to browser and browse this ip address. While browsing nginx default website will be shown.

## _Class 4 (GCP and Docker Networking with Monitoring)_
### _Topics: Aim & Workflow, IP monitoring from VM & IP monitoring from Container_
- **Aim & Workflow:** Aim of this class is to monitor IP trafiq under VM and Container from which we can understand the cloud network. In order to do so we use tcpdump at server side & tracert, curl -v in local. The workflow is being seperated into two parts
    - IP monitoring from VM
    - IP monitoring from container
- **IP monitoring from VM:** After setting VPC, VM, Firewall & nginx install tcpdump on VM. And from here start monitoring. The steps are given below.
    - sudo apt install net-tools
    - sudo apt install tcpdump
    - sudo ifconfig (Show linux network interfaces of VM)
    - sudo tcpdump -i {interface name} port {port number}
To check tcpdump response use the following command on local machine [cmd->adminstrator mode]
    - curl -v http://{ip address}
_Note:_ By doing so on local tcpdump will log some text on console as we are monitoring the linux interface.

- **IP monitoring from docker container:** After setting VPC, VM, Firewall install docker on VM. Create a nginx container and from inside the container start monitoring. The steps are given below.
    - sudo apt install docker
    - sudo apt install docker.io
    - sudo docker pull nginx (Pull image from docker-hub. Later we can use the same image from cache)
    - sudo docker run --name {container_name} -p 80:80 -d nginx
    - sudo docker images (Shows docker images)
    - sudo docker ps (Shows created containers)
    - sudo docker exec -it {container name} bash (Brings us to inside docker container)
After going inside container do following to monitory container interface through tcpdump
    - apt install net-tools
    - apt install tcpdump
    - ifconfig
    - tcpdump -i {interface name} port {port number}
To check tcpdump response use the following command on local machine [cmd->adminstrator mode]
    - curl -v http://{ip address}
_Note:_ By doing so on local tcpdump will log some text on console as we are monitoring the linux interface.

## _Class 6 & 7 (Google Cloud Storage)_
### _Topics: Transferable Cloud Storage_
- **Aim & Workflow:** Aim of this class is to store data in a remote storage and use that storage from different VM. To achieve follow this workflow: 
    1. Create VPC named **dod_web_network**
    2. Create a VM named **dod_web_vm_1**
    3. Create a persistance disk named **dod_web_disk**
    4. Add **dod_web_disk** disk to **dod_web_vm_1** VM instance
    5. Mount **dod_web_disk** disk to **dod_web_vm_1** VM instance
    6. Configuring automatic mounting on VM restart
    7. Install **mysql** and map data dir to **dod_web_disk** (/mnt/disks/sdb)
    8. Create database and populate Country table
    9. Check mysql data on **dod_web_disk** disk
    10. Disconnect **dod_web_disk** from **dod_web_vm_1**
    10. Create another VM named **dod_web_vm_2**
    12. Add **dod_web_disk** disk to **dod_web_vm_2** VM instance
    13. Mount **dod_web_disk** disk to **dod_web_vm_2** VM instance
    14. Install **mysql** and map data dir to **dod_web_disk** (/mnt/disks/sdb) for **dod_web_vm_2** VM
    15. Map data dir to **dod_web_disk**
    16. Check the created database and table

- **Create VPC named dod_web_network:** Please follow above procedure.
- **Create a VM named dod_web_vm_1:** Please follow above procedure.
- **Create a persistance disk named dod_web_disk:** Please follow the below procedure.
    - Search for _Disks_. Then click _Create Disk_.
    - Provide disk name as **dod_web_disk**
    - Provide region. Note: This should be under the same region of VM for getting maximum read write performance.
    - Disk Storage Type: According to preference (Blank disk default)
    - Disk Type: According to preference (SSD persistance disk default)
    - Size: As you wish
    - Select or create a snapshot schedule: default-schedule-1
    - Encryption: Google-managed encryption key
- **Add _dod_web_disk disk_ to _dod_web_vm_1_ VM instance:** Please follow the below procedure.
    - Open created **_dod_web_vm_1_** instance & click edit.
    - Now click on **ATTACH EXISTING DISK** and select **dod_web_disk**. 
    - Then save changes.
    - To check the disk as been added write **_sudo lsblk_** on VM console. This will show attached disk information. (named sdb). Note: The MOUNTPOINT will be empty right now.
- **Mount dod_web_disk disk to dod_web_vm_1 VM instance:** Please follow the below procedure.
    -  sudo mkfs.ext4 -m 0 -E lazy_itable_init=0,lazy_journal_init=0,discard /dev/sdb **(This command format the attached disk. Do this only when the disk is empty)**
    -  sudo mkdir -p /mnt/disks/dod_web **(This command create a mount dir)**
    -  sudo mount -o discard,defaults /dev/sdb /mnt/disks/dod_web **(This command mount sdb to /mnt/disks/dod_web dir)**
    -  sudo chmod a+w /mnt/disks/dod_web **(This command provides read write access to attached disk)**
    -  dh -h (Check mounted disk by this command)
- **Configuring automatic mounting on VM restart:** Please follow the below procedure. Note: This is needed as if for some reason VM restart.
    -  sudo cp /etc/fstab /etc/fstab.backup (Create a backup of your current /etc/fstab file. Just incase)
    -  sudo blkid /dev/sdb (Use the blkid command to list the UUID for the disk.)
    -  UUID=UUID_VALUE /mnt/disks/dod_web ext4 discard,defaults,nofail 0 2 (Open the /etc/fstab file in a text editor  (nano) and create an entry that includes the UUID. Note: The UUID value will come from sudo blkid command)
    -  cat /etc/fstab (Check the saved text by this command)

## Keywords
- AS: Autonomous System
- BGP: Border Gateway Protocal 
- CIDR: Classless Inter Domain Routing
- DHCP: Border Gateway Protocal
- IAP: Identity Aware Proxy
- NIC: Network Interface Controller
- NAT: Network Address Translation
- OSI: Open Systems Interconnection 
- TCP: Transmission Control Protocal 
- UDP: User Datagram Protocal
- VPC: Virtual Private Cloud
