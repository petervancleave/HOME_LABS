
# Introduction

A company's network defense starts with fortifying the Internet edge with firewalls, but it is equally important to use hardware for regulating network traffic that reveals no more information than is necessary. Those who want to break into network systems employ reconnaissance techniques, which might reveal information that they can exploit to penetrate the edge defense. Ultimately, the tools that network engineers use to troubleshoot network problems are the same tools you will use to identify and learn vulnerable points in your perimeter infrastructure.

In this lab, we will use 7 different tools:
- ARP (Address Resolution Protocol) - This is a network protocol used to determine hardware addresses (MAC) of a device based on the IP address. It can be used when a device wants to communicate with another device on a network or it can be used to set up network interfaces on devices.

-  Ipconfig/Ifconfig - This command displays all of the TCP/IP network configuration values within a computer, including default gateways and netmasks. It can be used to refresh the Dynamic Host Configuration Protocols (DHCP) and the Domain Name System (DNS) settings. This command can be used to enable and disable ethernet or other network adapters. This command is a Windows-only command. Ifconfig is the linux based command that functions nearly identical to ipconfig. It can be used to display TCP/IP information as well as default gateways and netmasks.

- Hping3 - This is an updated version of a legacy tool called hping, a well-known, well-used tool for network scanning and firewall testing. Hping3 can send ICMP-based ping probes and other customized TCP/IP packets.

- Ping - This command sends a request over the network to a specific device. The communication will either succeed (return packets to the host machine) or fail (no packets returned). The command can be used with an IP address or a URL.

-  Tcpdump - This tool, which has been around since 1987, was written by Van Jacobson, who also wrote traceroute. Tcpdump is a network analyzer that intercepts and displays TCP/IP packets and uses the libpcap library to capture packets.

- Nmap - Nmap is similar to hping3 but extends its functionality by an order of magnitude with respect to the packets and speed with which they’re sent. Nmap also has a GUI version called Zenmap. Developed by Gordon Lyon (also known by his pseudonym, Fyodor Vaskovich), it was first published in 1997. Nmap crafts packets that it injects into a network and then analyzes the responses to map machines, ports, and services.

- Wireshark - Wireshark is similar to tcpdump but provides a more granular GUI interface. This allows for capture filters and display filters of the packet flows that it captures. It can also open saved capture files in a number of formats.

<u>Lab Overview</u>

Section 1:
1. In the first part of the lab, you will use the ipconfig, ARP, and ping commands to explore the Local Area Network.  

2. In the second part of the lab, you will use Nmap/Zenmap and Wireshark to capture and analyze network traffic.

Section 2:
Apply what was learned in section 1 with less guidance and different deliverables, as well as expanded tasks and alternative methods. Explore the WAN and use different tools for analyzing network traffic.

Section 3:
Explore the virtual environment to answer a set of questions and challenges that allow you to use the skills you learned in the lab to conduct independent, unguided work - similar to what might be encountered in a real-world situation.

<img width="1435" height="827" alt="Screenshot 2025-09-07 161154" src="https://github.com/user-attachments/assets/00c6596e-750e-4b33-a6e5-7fde5d1f945f" />

<u>Learning Objectives</u>

1. Identify IP addresses, MAC addresses, and subnet masks using network utilities.  
2. Generate customized TCP/IP packets, with varying speed and purpose.  
3. Capture network traffic for the purpose of analysis and investigation.  
4. Apply appropriate filters to view only the traffic subset of interest.  
5. Analyze network traffic to determine the configuration of running applications on the IP hosts from which traffic is captured.

<u>Topology</u>

The following virtual machines will be used:
- vWorkstation (Windows Server 2019)
- TargetWindows01 (Windows Server 2019)
- TargetLinux01 (Ubuntu Linux)
- pfSense
- AttackLinux01 (Kali Linux)
- RemoteWindows01 (Windows Server 2019)

<img width="937" height="555" alt="Screenshot 2025-09-07 163038" src="https://github.com/user-attachments/assets/0a32c8cc-d009-4ba6-b684-f1eb7453b06e" />

# Section 1,

<u>Part 1 - Explore the Local Area Network</u>

On the vWorkstation taskbar, **click** the **Command Prompt icon** to open a new Command Prompt window.

At the command prompt, **type ipconfig** and **press Enter** to display basic information about the vWorkstation’s network adapters.

<img width="1417" height="626" alt="Screenshot 2025-09-07 163925" src="https://github.com/user-attachments/assets/f1cad158-4bf5-4b20-9857-2bb03822e2db" />


  
At the command prompt, **type ipconfig /all** and **press Enter** to display detailed information about the vWorkstation’s network adapters.

<img width="1680" height="718" alt="Screenshot 2025-09-07 164042" src="https://github.com/user-attachments/assets/ed88a0a1-6653-4e27-9763-ab4f124417b6" />


vWorkstation
```cmd
Ethernet adapter Student:

   Connection-specific DNS Suffix  . :
   Description . . . . . . . . . . . : vmxnet3 Ethernet Adapter #3
   Physical Address. . . . . . . . . : 00-50-56-BD-31-02
   DHCP Enabled. . . . . . . . . . . : No
   Autoconfiguration Enabled . . . . : Yes
   IPv4 Address. . . . . . . . . . . : 172.30.0.2(Preferred)
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . : 172.30.0.1
   DNS Servers . . . . . . . . . . . : 172.30.0.10
   NetBIOS over Tcpip. . . . . . . . : Enabled
```


On the Lab View toolbar, **select TargetWindows01** from the Virtual Machine drop-down menu to connect to the TargetWindows01 machine.

**Repeat steps 1-3** on TargetWindows01.

<img width="1438" height="810" alt="Screenshot 2025-09-07 164435" src="https://github.com/user-attachments/assets/3939a69c-5e90-48fd-bcb2-f4a6911bf3d2" />

TargetWindows01
```cmd
C:\Users\Administrator>ipconfig

Windows IP Configuration


Ethernet adapter TrueLab:

   Connection-specific DNS Suffix  . :
   IPv4 Address. . . . . . . . . . . : 192.168.205.2
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . : 192.168.205.254

Ethernet adapter Student:

   Connection-specific DNS Suffix  . :
   Link-local IPv6 Address . . . . . : fe80::9d00:c31c:993f:228b%5
   IPv4 Address. . . . . . . . . . . : 172.30.0.10
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . : 172.30.0.1

C:\Users\Administrator>ipconfig /all

Windows IP Configuration

   Host Name . . . . . . . . . . . . : TargetWindows01
   Primary Dns Suffix  . . . . . . . : securelabsondemand.com
   Node Type . . . . . . . . . . . . : Hybrid
   IP Routing Enabled. . . . . . . . : No
   WINS Proxy Enabled. . . . . . . . : No
   DNS Suffix Search List. . . . . . : securelabsondemand.com

Ethernet adapter TrueLab:

   Connection-specific DNS Suffix  . :
   Description . . . . . . . . . . . : vmxnet3 Ethernet Adapter
   Physical Address. . . . . . . . . : 00-50-56-BD-26-EF
   DHCP Enabled. . . . . . . . . . . : No
   Autoconfiguration Enabled . . . . : Yes
   IPv4 Address. . . . . . . . . . . : 192.168.205.2(Preferred)
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . : 192.168.205.254
   NetBIOS over Tcpip. . . . . . . . : Disabled

Ethernet adapter Student:

   Connection-specific DNS Suffix  . :
   Description . . . . . . . . . . . : vmxnet3 Ethernet Adapter #3
   Physical Address. . . . . . . . . : 00-50-56-BD-86-ED
   DHCP Enabled. . . . . . . . . . . : No
   Autoconfiguration Enabled . . . . : Yes
   Link-local IPv6 Address . . . . . : fe80::9d00:c31c:993f:228b%5(Preferred)
   IPv4 Address. . . . . . . . . . . : 172.30.0.10(Preferred)
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . : 172.30.0.1
   DHCPv6 IAID . . . . . . . . . . . : 167792726
   DHCPv6 Client DUID. . . . . . . . : 00-01-00-01-30-4F-B8-24-00-50-56-BD-26-EF
   DNS Servers . . . . . . . . . . . : 127.0.0.1
   NetBIOS over Tcpip. . . . . . . . : Enabled
```

On the Lab View toolbar, **select vWorkstation** from the Virtual Machine drop-down menu to connect to the vWorkstation machine.

At the command prompt, **type arp** and **press Enter** to display the help guide for the ARP utility.

<img width="865" height="788" alt="Screenshot 2025-09-07 164610" src="https://github.com/user-attachments/assets/9173653b-e809-4276-bce1-ec761189156c" />

At the command prompt, **type arp -a** and press Enter to display the current ARP cache for the vWorkstation.

```cmd
C:\Users\Administrator>arp -a

Interface: 192.168.205.4 --- 0xd
  Internet Address      Physical Address      Type
  192.168.205.254       00-50-56-ab-66-1c     dynamic
  192.168.253.254       00-50-56-ab-66-1c     dynamic
  224.0.0.22            01-00-5e-00-00-16     static
  224.0.0.251           01-00-5e-00-00-fb     static
  224.0.0.252           01-00-5e-00-00-fc     static
  255.255.255.255       ff-ff-ff-ff-ff-ff     static

Interface: 172.30.0.2 --- 0x11
  Internet Address      Physical Address      Type
  172.30.0.1            00-50-56-bd-14-0f     dynamic
  172.30.0.10           00-50-56-bd-86-ed     dynamic
  172.30.0.255          ff-ff-ff-ff-ff-ff     static
  224.0.0.22            01-00-5e-00-00-16     static
  224.0.0.251           01-00-5e-00-00-fb     static
  224.0.0.252           01-00-5e-00-00-fc     static
  255.255.255.255       ff-ff-ff-ff-ff-ff     static
```

At the command prompt, **type arp -d** and **press Enter** to clear the ARP cache.

```cmd
arp -d
```

At the command compt, **type arp -a** and **press Enter** to display the updated ARP cache.

```cmd
C:\Users\Administrator>arp -a

Interface: 192.168.205.4 --- 0xd
  Internet Address      Physical Address      Type
  192.168.205.254       00-50-56-ab-66-1c     dynamic
  224.0.0.22            01-00-5e-00-00-16     static

Interface: 172.30.0.2 --- 0x11
  Internet Address      Physical Address      Type
  224.0.0.22            01-00-5e-00-00-16     static
```

At the command prompt, **type ping 172.30.0.10** and **press Enter** to ping the TargetWindows01 machine.

```cmd
C:\Users\Administrator>ping 172.30.0.10

Pinging 172.30.0.10 with 32 bytes of data:
Reply from 172.30.0.10: bytes=32 time<1ms TTL=128
Reply from 172.30.0.10: bytes=32 time<1ms TTL=128
Reply from 172.30.0.10: bytes=32 time<1ms TTL=128
Reply from 172.30.0.10: bytes=32 time<1ms TTL=128

Ping statistics for 172.30.0.10:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms
```

At the command prompt, **type arp -a** and **press Enter** to display the updated ARP cache.
The ARP cache should now once again contain an entry for TargetWindows01.

```cmd
C:\Users\Administrator>arp -a

Interface: 192.168.205.4 --- 0xd
  Internet Address      Physical Address      Type
  192.168.205.254       00-50-56-ab-66-1c     dynamic
  224.0.0.22            01-00-5e-00-00-16     static

Interface: 172.30.0.2 --- 0x11
  Internet Address      Physical Address      Type
  172.30.0.1            00-50-56-bd-14-0f     dynamic
  172.30.0.10           00-50-56-bd-86-ed     dynamic
  172.30.0.255          ff-ff-ff-ff-ff-ff     static
  224.0.0.22            01-00-5e-00-00-16     static
```

At the command prompt, **type exit** and **press Ente**r to close the command prompt window.

On the vWorkstation desktop, **double-click** the **NetworkAssessment file** to open it in OpenOffice Calc.

<img width="645" height="736" alt="Screenshot 2025-09-07 165401" src="https://github.com/user-attachments/assets/d37bad18-077d-4043-907e-7a0bac19b980" />

**Complete** the **LAN tab** using the information obtained from the ipconfig and ARP utilities.

(We can do this using ipconfig /all and arp -a)

<img width="1906" height="775" alt="Screenshot 2025-09-07 170054" src="https://github.com/user-attachments/assets/67a675b5-e3ab-4f57-9be3-8a331b835538" />

<u>Part 2 - Analyze Network Traffic</u>

On the vWorkstation desktop, **double-click** the **Wireshark icon** to open the Wireshark application.

<img width="760" height="831" alt="Screenshot 2025-09-07 170436" src="https://github.com/user-attachments/assets/96d639ff-68b8-4fa8-8a2a-08dea1afd79d" />

In the Wireshark window, **click** the **Student interface** to select the network interface that Wireshark will use to capture traffic.

From the Wireshark toolbar, **click** the **Start Capture button (the blue shark fin)** to begin the capture session.

<img width="1757" height="772" alt="Screenshot 2025-09-07 170541" src="https://github.com/user-attachments/assets/ef2f6311-7cb4-4cf0-b0ce-2b7367b0165d" />

**Minimize** the **Wireshark window**.

On the vWorkstation desktop, **double-click** the **Nmap - Zenmap GUI icon** to open the Zenmap application.

On the vWorkstation desktop, **double-click** the **Nmap - Zenmap GUI icon** to open the Zenmap application.

<img width="552" height="762" alt="Screenshot 2025-09-07 170654" src="https://github.com/user-attachments/assets/5fe61d75-9dc3-44d1-bab7-e8c7b5f789ab" />

In the Zenmap window, **type 172.30.0.1** (the internal firewall interface) in the _Target_ box and **select Ping scan** from the Profile drop-down menu, then **click Scan** to start the scan.

<img width="721" height="545" alt="Screenshot 2025-09-07 170737" src="https://github.com/user-attachments/assets/1eca649c-1e45-4a91-89a2-a363a898a8f8" />

**Restore** the **Wireshark window**.

In the Wireshark window, **type icmp** in the Filter box and **press Enter** to filter the results to show only the ping traffic.

<img width="1915" height="780" alt="Screenshot 2025-09-07 170841" src="https://github.com/user-attachments/assets/622b9450-bf10-4c11-b9cf-3ef7ab896695" />

On the Wireshark toolbar, **click** the **Clear button** (the x) to remove the ICMP filter, then **type arp** in the Filter box and **press Enter** to filter the results to show only ARP-related traffic.

<img width="1896" height="813" alt="Screenshot 2025-09-07 170913" src="https://github.com/user-attachments/assets/d84f3fb0-94fc-4dd2-a1df-d91c09aaf64d" />

**Review** the ARP packet results and **locate** a packet that lists the vWorkstation as the source and the firewall’s internal interface as the destination.

We can do so by identifying the vWorkstation using its MAC address.

00-50-56-BD-31-02

<img width="1867" height="642" alt="Screenshot 2025-09-07 171211" src="https://github.com/user-attachments/assets/0d3a0818-3e74-46af-a71e-5e0fa37a2500" />

On the Wireshark toolbar, **click** the **Clear button** to remove the ARP filter.

**Restore** the **Zenmap window**.

In the Zenmap window, **select Regular scan** from the Profile drop-down list and **click Scan** to start a new scan.  
  
If you did not minimize the Wireshark window, you should see the traffic generated by nmap captured in real-time.

<img width="1912" height="822" alt="Screenshot 2025-09-07 171347" src="https://github.com/user-attachments/assets/4db65e1b-c28d-4c1b-8be0-bc1b402043a5" />

**Repeat steps 8 and 10** to observe whether the Regular scan generated additional ICMP and ARP traffic.

<img width="1900" height="827" alt="Screenshot 2025-09-07 171418" src="https://github.com/user-attachments/assets/00988311-4f69-4d0f-ace8-497a001d4e71" />

In the Zenmap window, **select Intense scan** from the Profile drop-down list and **click Scan** to start a new scan.

*This scan will take several minutes to complete. If you did not minimize the Wireshark window, you should see the traffic generated by nmap captured in real-time. While the scan is running, compare the command for this scan with that of the Ping scan. In this case, Nmap is directed to scan the IP address (**172.30.0.1**) as quickly as possible (**-T4**), to attempt to detect the operating system (**-A**), and to return as much information (verbose results) as it can (**-v**). You should notice that Wireshark has already captured substantially more traffic than the prior two scans.*

<img width="1905" height="825" alt="Screenshot 2025-09-07 171522" src="https://github.com/user-attachments/assets/69e15e63-156b-40d3-a81c-f4cd3a8aa3a7" />

When the scan is complete, **restore** the **Wireshark window**.

**Repeat steps 8 and 10** to observe whether the Intense scan generated additional ICMP and ARP traffic.

<img width="1912" height="821" alt="Screenshot 2025-09-07 171649" src="https://github.com/user-attachments/assets/3268e511-4615-480d-a980-1b56da241e2d" />

<img width="1682" height="60" alt="Screenshot 2025-09-07 171713" src="https://github.com/user-attachments/assets/8505b39c-170d-46cc-9927-d3ffc0ea4125" />

From the Wireshark tool bar, **click** the **Stop icon** to end the capture session

**Restore** the **Zenmap window**.

In the Zenmap window, **click** the **Ports/Hosts tab** to see which ports are open and listening.

<img width="922" height="722" alt="Screenshot 2025-09-07 171819" src="https://github.com/user-attachments/assets/8431b2f2-da22-4a9d-959c-cfccebb025b4" />

End Section 1

# Section 2

<u>Part 1 - Explore the WAN</u>

Use the Virtual Machine menu to **connect** to the **AttackLinux01 machine**.

<img width="1905" height="826" alt="Screenshot 2025-09-07 172000" src="https://github.com/user-attachments/assets/bdfaadea-2419-47a6-bd97-143b61d16cda" />

At the AttackLinux01 login page, use the following credentials to **log in**:  
  
Username: **root**  
Password: **toor**

From the AttackLinux01 menu bar, **click** the **Activities menu**, then **click** the **Terminal icon** on the Applications bar to open a new Terminal window.

<img width="1013" height="757" alt="Screenshot 2025-09-07 172057" src="https://github.com/user-attachments/assets/e1d61359-5f66-4c12-a733-d5e5ed7880ff" />

At the command prompt, **execute ifconfig** to display information about AttackLinux01’s default network adapter.

<img width="952" height="715" alt="Screenshot 2025-09-07 172208" src="https://github.com/user-attachments/assets/da08387d-e9ba-44e3-80f5-9c0e339d7202" />

At the command prompt, **execute ifconfig -a** to display information about all of AttackLinux01’s network adapters.

*While AttackLinux01 has no additional network adapters to display, the **-a** switch is the ifconfig equivalent of the **/all** switch on Windows.*

<img width="850" height="627" alt="Screenshot 2025-09-07 172342" src="https://github.com/user-attachments/assets/fb694283-1440-45e5-8cdb-95a92a28c6f3" />

**Close** the **Terminal window**.

Use the Virtual Machine menu to **connect** to the **RemoteWindows01 machine**

From the RemoteWindows01 taskbar, **open** a new **command prompt window**

At the command prompt, **execute the command** to display information about RemoteWindows01’s default network adapter.

```cmd
C:\Users\Administrator>ipconfig

Windows IP Configuration


Ethernet adapter Student:

   Connection-specific DNS Suffix  . :
   Link-local IPv6 Address . . . . . : fe80::5969:38ab:fcdc:5977%11
   IPv4 Address. . . . . . . . . . . : 10.0.1.2
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . : 10.0.1.1

Ethernet adapter TrueLab:

   Connection-specific DNS Suffix  . :
   IPv4 Address. . . . . . . . . . . : 192.168.205.1
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . : 192.168.205.254
```

At the command prompt, **execute the command** to display the ARP cache for RemoteWindows01.  
  
```cmd
C:\Users\Administrator>arp -a

Interface: 10.0.1.2 --- 0xb
  Internet Address      Physical Address      Type
  10.0.1.1              00-50-56-bd-db-47     dynamic
  10.0.1.255            ff-ff-ff-ff-ff-ff     static
  224.0.0.22            01-00-5e-00-00-16     static
  224.0.0.251           01-00-5e-00-00-fb     static
  224.0.0.252           01-00-5e-00-00-fc     static

Interface: 192.168.205.1 --- 0xe
  Internet Address      Physical Address      Type
  192.168.205.254       00-50-56-ab-66-1c     dynamic
  192.168.253.254       00-50-56-ab-66-1c     dynamic
  224.0.0.22            01-00-5e-00-00-16     static
  224.0.0.251           01-00-5e-00-00-fb     static
  255.255.255.255       ff-ff-ff-ff-ff-ff     static
```

At the command prompt, **execute the command** to clear the ARP cache.

```cmd
C:\Users\Administrator>arp -d

C:\Users\Administrator>arp -a

Interface: 10.0.1.2 --- 0xb
  Internet Address      Physical Address      Type
  224.0.0.22            01-00-5e-00-00-16     static

Interface: 192.168.205.1 --- 0xe
  Internet Address      Physical Address      Type
  192.168.205.254       00-50-56-ab-66-1c     dynamic
  224.0.0.22            01-00-5e-00-00-16     static
```

At the command prompt, **execute the command** to ping the protected network's external firewall IP address at 202.20.1.1.

```cmd
C:\Users\Administrator>ping 202.20.1.1

Pinging 202.20.1.1 with 32 bytes of data:
Reply from 202.20.1.1: bytes=32 time=3ms TTL=63
Reply from 202.20.1.1: bytes=32 time=2ms TTL=63
Reply from 202.20.1.1: bytes=32 time=3ms TTL=63
Reply from 202.20.1.1: bytes=32 time=3ms TTL=63

Ping statistics for 202.20.1.1:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 2ms, Maximum = 3ms, Average = 2ms
```

At the command prompt, **execute the command** to display the updated ARP cache.  
  
The ARP cache for the Student network interface should now contain an entry for the RemoteWindows01 machine's default gateway (10.0.1.1).

```cmd
Interface: 10.0.1.2 --- 0xb
  Internet Address      Physical Address      Type
  10.0.1.1              00-50-56-bd-db-47     dynamic
  10.0.1.255            ff-ff-ff-ff-ff-ff     static
  224.0.0.22            01-00-5e-00-00-16     static

Interface: 192.168.205.1 --- 0xe
  Internet Address      Physical Address      Type
  192.168.205.254       00-50-56-ab-66-1c     dynamic
  224.0.0.22            01-00-5e-00-00-16     static
```

Use the Virtual Machine menu to **connect** to the **vWorkstation machine**.

**Restore** or **re-open** the **NetworkAssessment file**.

**Complete** the **WAN tab** using the information obtained from the if/ipconfig and arp utilities.

```cmd
C:\Users\Administrator>ipconfig /all

Windows IP Configuration

   Host Name . . . . . . . . . . . . : RemoteWindows01
   Primary Dns Suffix  . . . . . . . :
   Node Type . . . . . . . . . . . . : Hybrid
   IP Routing Enabled. . . . . . . . : No
   WINS Proxy Enabled. . . . . . . . : No

Ethernet adapter Student:

   Connection-specific DNS Suffix  . :
   Description . . . . . . . . . . . : vmxnet3 Ethernet Adapter #3
   Physical Address. . . . . . . . . : 00-50-56-BD-E9-E9
   DHCP Enabled. . . . . . . . . . . : No
   Autoconfiguration Enabled . . . . : Yes
   Link-local IPv6 Address . . . . . : fe80::5969:38ab:fcdc:5977%11(Preferred)
   IPv4 Address. . . . . . . . . . . : 10.0.1.2(Preferred)
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . : 10.0.1.1
   DHCPv6 IAID . . . . . . . . . . . : 469782614
   DHCPv6 Client DUID. . . . . . . . : 00-01-00-01-30-4F-B8-50-00-50-56-BD-E9-E9
   DNS Servers . . . . . . . . . . . : fec0:0:0:ffff::1%1
                                       fec0:0:0:ffff::2%1
                                       fec0:0:0:ffff::3%1
   NetBIOS over Tcpip. . . . . . . . : Enabled

Ethernet adapter TrueLab:

   Connection-specific DNS Suffix  . :
   Description . . . . . . . . . . . : vmxnet3 Ethernet Adapter #2
   Physical Address. . . . . . . . . : 00-50-56-BD-5E-E7
   DHCP Enabled. . . . . . . . . . . : No
   Autoconfiguration Enabled . . . . : Yes
   IPv4 Address. . . . . . . . . . . : 192.168.205.1(Preferred)
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . : 192.168.205.254
   NetBIOS over Tcpip. . . . . . . . : Disabled
```

<img width="1356" height="785" alt="Screenshot 2025-09-07 173618" src="https://github.com/user-attachments/assets/353381d6-9d11-4880-9206-426c63966fba" />

<u>Part 2 - Analyze Network Traffic</u>

Using the Virtual Machine menu, **connect** to the **AttackLinux01 machine**.

From the AttackLinux01 menu bar, **open** a new **Terminal window**.

At the command prompt, **execute hping3 -h** to open the help screen for hping3.

<img width="797" height="592" alt="Screenshot 2025-09-07 173752" src="https://github.com/user-attachments/assets/6ef5e051-4cd4-4648-b3fa-c11ee91bb741" />

At the command prompt, **execute hping3 -1 -c 1 202.20.1.1**.

*This command uses ICMP mode (**-1**) to send a single packet (**-c 1**) to the external interface of the pfSense firewall/router (**202.20.1.1**).*


<img width="862" height="217" alt="Screenshot 2025-09-07 173828" src="https://github.com/user-attachments/assets/f1f84e3e-8c3e-4a88-8e33-4ff65b906084" />

From the menu bar, **open** a second **Terminal window**.

At the command prompt in the second terminal window, **execute tcpdump -h**.
*As with hping3, adding the **-h** switch provides guidance on the available switches and parameters.*

<img width="1052" height="705" alt="Screenshot 2025-09-07 173930" src="https://github.com/user-attachments/assets/b910df42-1113-44ad-a34c-0d13e7a26072" />

In the tcpdump window, **execute tcpdump -i eth0 -n host 202.20.1.1** to collect packets as they are transmitted to the IP address 202.20.1.1.

<img width="1183" height="707" alt="Screenshot 2025-09-07 174028" src="https://github.com/user-attachments/assets/0692e9b8-bcf2-4440-83f1-eadd906f845e" />

In the hping3 window, **execute hping3 -1 -c 1 202.20.1.1** to send another ICMP packet to the external firewall interface

*In the tcpdump window, you will see tcpdump echo back the captured packets. There are two pairs of packets. The first two packets are the ICMP echo request and the ICMP echo reply. The second pair of packets consists of an Address Resolution Protocol (ARP) request and an ARP reply providing the MAC address of the firewall.*

<img width="1082" height="662" alt="Screenshot 2025-09-07 174300" src="https://github.com/user-attachments/assets/b9e28240-208e-4846-acdc-9a27cafcc54b" />

<img width="808" height="198" alt="Screenshot 2025-09-07 174347" src="https://github.com/user-attachments/assets/75dbe9d0-796e-44a1-9486-b96be5994f12" />

In the hping3 terminal window, **execute hping3 -S -c 1 -s 5151 202.20.1.1** to send a single (**-c 1**) SYN packet (**-S**), directed to the firewall (**202.20.1.1**) on source port (**-s**) 5151.

*Notice that the tcpdump output shows the SYN packet sent (Flags [S]) from the Kali machine to the firewall, but with no response. The destination port was not listening. Because hping3 is sending the packet without a specified destination port, you should not expect any response.*

<img width="782" height="462" alt="Screenshot 2025-09-07 174502" src="https://github.com/user-attachments/assets/85359fd4-6139-4b22-b78b-17f089336d16" />

<img width="815" height="215" alt="Screenshot 2025-09-07 174534" src="https://github.com/user-attachments/assets/62eadf5e-40ff-4fd3-941b-9d4ae123aaee" />

In the hping3 window, **type hping3 -S -c 1 -s 5151 -p 80 202.20.1.1** and **press Enter** to send the same packet to a specific destination port (**-p 80**) that should be listening.

*In the tcpdump window, the output shows the attempted three-way handshake. The firewall’s port 80 was listening and responded with a SYN/ACK. In a normal connection request, the third ACK packet would be sent. However, because hping3 did not intend to establish a connection, it instead sent the firewall a reset (R) packet, closing the connection request. Now you know that port 80 is active and listening. You could use this same technique to assess every individual port on a system, but doing so manually would be very tedious and time-consuming, and would be better accomplished by using a tool like Nmap. Nonetheless, it is valuable to observe and understand the transaction and handshake process at the packet level.*

<img width="1185" height="648" alt="Screenshot 2025-09-07 174613" src="https://github.com/user-attachments/assets/ccbdf976-3649-4781-b4f1-1b73160d825b" />

<img width="896" height="372" alt="Screenshot 2025-09-07 174629" src="https://github.com/user-attachments/assets/d80951dd-dbca-4a68-92fd-91b3911490a4" />

In the hping3 window, **execute exit** to close the window.

In the tcpdump window, **press Ctrl+C** to cancel listening mode and return to the command prompt.

At the command prompt, **execute telnet 202.20.1.1 80** to request a telnet connection to the pfSense firewall-router on port 80.  
  
*The system will return a message indicating that a Telnet connection was made (connected to 202.20.1.1).*

<img width="938" height="562" alt="Screenshot 2025-09-07 174814" src="https://github.com/user-attachments/assets/3bafe2c2-deb0-46f7-ac6a-1617b7d4ccad" />

**Execute get** to return a response from the web service.

*You should be able to see the type and version of the Web server running. This technique for enumerating information about the service running is called banner grabbing.*

<img width="943" height="573" alt="Screenshot 2025-09-07 174833" src="https://github.com/user-attachments/assets/21b7f845-c286-45f9-8ef9-ca9e16c55d23" />

End Section 2

# Section 3

<u>Part 1 - Explore the DMZ</u>

As a first step, you will need to expand your network assessment to one more area of the network that you have not previously explored - the DMZ, or De-militarized Zone. The term "DMZ" is used to describe a network segment that is separate from the tightly-guarded Private Network or LAN. The DMZ is typically used to house servers that must be exposed to the public Internet - for example, web servers - and therefore require a less restrictive firewall policy than other parts of a network. In this case, the DMZ contains one server - TargetLinux01. Connect to TargetLinux01, then gather the information required to complete the DMZ tab of the NetworkAssessment spreadsheet on the vWorkstation.

So we need to retrieve the IP, Subnet Mask, MAC, and Default Gateway of the TargetLinux01 Machine...

we can do so by running:

```shell
ifconfig -a
```

<img width="1182" height="767" alt="Screenshot 2025-09-07 175159" src="https://github.com/user-attachments/assets/6d7cc75d-81cf-45f5-ba29-2985bffdd2b1" />

<img width="1750" height="825" alt="Screenshot 2025-09-07 175312" src="https://github.com/user-attachments/assets/57a89d1b-e58a-4915-b38d-b937be24771c" />

<u>Part 2 - Perform Reconnaissance on the Firewall</u>

Next, you will need to conduct some additional reconnaissance on the firewall itself. From the AttackLinux01 machine, start a tcpdump or Wireshark capture, then run a Regular scan of the pfSense firewall’s external interface. Analyze the capture and consider the following questions.

- Were any ICMP packets sent to the firewall?
- Were any ARP packets sent to the firewall?
- Were any DNS packets sent to the firewall?
- What ports are open on the pfSense firewall?

<img width="1027" height="581" alt="Screenshot 2025-09-07 175913" src="https://github.com/user-attachments/assets/763d9000-f1e0-480b-a910-eb3c3506dfbd" />
<img width="1207" height="637" alt="Screenshot 2025-09-07 175842" src="https://github.com/user-attachments/assets/05aad2c7-3b8c-4281-9074-262885259a70" />
<img width="1201" height="692" alt="Screenshot 2025-09-07 175825" src="https://github.com/user-attachments/assets/0bf4df4c-e29b-4e15-954a-63756402b20f" />
<img width="1122" height="711" alt="Screenshot 2025-09-07 175805" src="https://github.com/user-attachments/assets/fbd391eb-d535-475e-b4ac-74eb368009b4" />
<img width="1361" height="647" alt="Screenshot 2025-09-07 175743" src="https://github.com/user-attachments/assets/b935c4d6-9fc8-4614-a3a1-f95d45e07b79" />

