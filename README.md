
# Poridhi DevOps Documentation
## _Course Syllabus_

Following topics will be discussed in this course.
- DevOps Google Clound
-- Basic Networking
-- Cloud Networking
-- Docker Networking
- Application Component
-- MySql
-- Nginx
-- Microservice with Docker Compose
- Project

## _Basic Networking_
- **About OS Space & NIC:** VM (Virtual Machine) has two spaces. One _User Space_ and another _Kernel Space_. _User Space_ contains applications which communicate with _Network stack_. Communication is done through data packet. _Network stack_ sends the data packet to _NIC (Network Interface Controller)_ and this NIC send that outside. Follow the example below:-

![N|NIC](https://drive.google.com/uc?export=view&id=1QYyFaLwPO8yW4dVeB37xsCNRhP1WHg4L)

- **IP Address:** IP Address has four blocks. We call each block as _octate_. Each block has 8 bits. Number range foreach block is between (0 - 255). In total IP address consume 32 bits (4 * 8 bits). IP Address has two parts. _Host part_ and _Network part_. _(Note: To allocate all users IP addresses we need NAT. Later we will discuss about it)_. Now, IP Address has two range. _Public Range_ and _Private Range_. This public range has been splited into different region. We call it as _Subnet_.To represent subnet first Class A, Class B, Class C, ... notations were used. But later a very popular notation were used and that is _CIDR (Classless inter domain routing)_.

- **Subnet and Subnet Mask:** A network connecting the host interfaces and one router interface having the same IP address format is called _Subnet_. It is represented as a.b.c.d/x where _/x_ is called as Subnet Mask. 

- **NAT (Network Address Translation):** Network Address Translation or NAT is a process where it converts Private IP Address to Public and Public to Private. Through this private IP Addresses can communicate with public IP Address. To maintain conversion NAT uses _NAT Translation Table_ where it maps Private and Public IP Addresses. 

- **CIDR (Classless Inter Domain Routing):** CIDR notation looks something like this _12.13.0.0/16_. CIDR notation has two parts. One _Network_ and other _Host_. Now, here _12.13_ is the _Network_ part and _0.0_ is the _Host_ part. Also, 16 represents occupied bits by the _Network_ part. So, under a network 2^16 - 2 host addresses can be provided.

## _Layer 2 Devices:_
- **Hub:** Hub is a network connection among devices. In past we need to manually define IP addresses foreach machine that are conected to that _Hub_. For this, we need to maintain a table by hand. If not then that will increase the change of over lapping IP addresses.

![N|NIC](https://lh5.googleusercontent.com/jhn6vIbclGHnxUzfARn81TuIDcXhI5LDshx_gATq2CWyxcED-vG22rS_I8GMQhGx3TgxdSNdABQ1tulChGhX=w1366-h657)

- **DHCP:** In order to overcome this manual situation DHCP is being introduced. DHCP contains a HashMap (MAC, IP Address). This thing dynamically provide IP Address to a MAC. See the example below. Note: If we ping under same network then data packet will not go out of NIC card of the switch.

- **Switch:** Switch is an ungrade version of _Hub_. Its being used for inter device communication. It maintains a _MAC_ table. Now, If we ping 12.13.0.3 from Device 1  then this request will request DHCP for the MAC. Then we get BBB MAC address. Now, switch will try to find the MAC in MAC table and its related port information. After that the connection is being established.

![N|NIC](https://lh6.googleusercontent.com/SGVOTuA8R6kCxeUGOGcIgXulg7Gz0yT3wwZp5e6ss_XSBw3uiYCsUXghXgvLR7njTt5ivleCyLN9HT_ZdDeW=w1366-h657-rw)

## _Layer 3 Devices:_
- **Router:** Router is being used for inter network communication. Now if we ping outside the network the what will happen? See the example below. As D1 ping 10.15.0.2 which is not under S1 switch network then the data pack will go out of the gateway to router. Then it will try to find 10.15.0.0 under the table which is RI2 interface. Then the data pack will go to S2 switch to D2 device. By this way the connection is being established.

![N|NIC](https://lh6.googleusercontent.com/SIb2Jh8j_zbrFAPSLiK-B0ohcvuSKblCo93tsUX6um-xMiKPQXSmLY7Ae5ipNC3AH4CT8rQPnPU6u-BTsjfe=w811-h657-rw)
