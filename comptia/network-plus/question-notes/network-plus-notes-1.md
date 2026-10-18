	
# April 13th
## Question1; Bethany, a network administrator, wants to ensure that IP addresses are not tied up indefinitely by devices that are no longer active on the network. Which DHCP feature would allow her as an administrator to control the period a device can use an assigned IP address?

### 1.Scope 2.Lease Time 3.Options 4.Exclusions

Network Services - DHCP
tide up indefinitely, IP address exhaustion, 
Search[[DHCP]] setting,
DHCP Lease ... lease time expires, Options ... additional configurations to clients, Exclusions... exclude specific IP address

## Question2; Mathan has just purchased a domain name and created an A record to bind his domain name to an IP address. Which of the following tools should he use to verify the record was created properly?

### 1.dig 2.ipconfig 3.arp 4.tcpdump

The arp command is used to view and modify the local address resolution protocol (ARP) cache of a device.  The tcpdump tool is a text-based packet capture and analysis tool that can capture packets and display the contents of a packet capture (pcap) file. The ipconfig command is used on Windows devices to display the current TCP/IP network configuration and refresh the DHCP and DNS settings on a given host

## Question3; A network technician has received reports of an Internet-based application that has stopped functioning. Employees reported that after updating the Internet browsers, the application began to fail. Many users rolled back the update, but this did not correct the issue. What should the company do to reduce this type of action from causing network problems in the future?

### 1.Verify the update hashes match those on the vendor’s website 2.Segment the network and create a test lab for all updates before deployment 3.Coordinate the Internet server's update to coincide with the users’ updates 4.Implement a disaster recovery plan with a hot site to allow users to continue working

This question ask preventive measure. 1 is How to check if update files have been tampered with 3 is version of server and user but we don't know company control server. 4 is about Disaster Recovery.
## Qusestion4; Which of the following cloud infrastructures includes on-premise servers utilizing a centralized Syslog server hosted at a third-party organization to review the logs?

### 1.Hybrid 2.Community 3.Public 4.Private

205page, Syslog server logs from devices are sent

## Question5; A malicious user is blocking cellular devices from connecting to the Internet whenever they enter the coffee shop. If they get their coffee to go and walk at least a block away from the coffee shop, their smartphones will connect to the Internet again. What type of network attack is the malicious user performing?
### 1.Spoofing2.On-path attack3.Blacklisting IP addresses in the ACL4.Frequency jamming
#### Frequency jamming is one of the many exploits used to compromise a wireless environment. Frequency jamming is the disruption of radio signals through use of an over-powered signal in the same frequency range. It works by denying service to authorized users as legitimate traffic is jammed by the overwhelming frequencies of illegitimate traffic. There is no indication that the malicious user has created a rogue AP (which is a form of spoofing) or performing an on-path attack by having users connect through their laptop or device within this scenario. Also, there is no mention of certain websites or devices being blocked logically using a block-list or ACL. ACL is access control lists that permit or deny traffic based on IP/MAC address or port depending on device.
# April 14th
## Q1; You are assisting a member of Dion Training's security team during an incident response. The team member asks you to determine if any strange TCP connections are occurring on a given workstation. You open the command prompt on the workstation. Which of the following tools would provide you with information on any TCP connections currently established on the workstation?
### 1.route2.arp3.tracert4.netstat
####  netstat is useful when determining if a workstation is attempting outbound connections due to malware (beaconing activity) or has ports open and listening for inbound connections. The route command is used to create, view, or modify manual entries in the network routing tables of a computer or server. The route command is used to create, view, or modify manual entries in the network routing tables of a computer or server.
## Q2; A network technician at a warehouse must implement a solution that will allow a company to track shipments as they enter and leave the facility. The warehouse workers must scan each package as it enters the warehouse using a sensor that can reach a distance of up to 30cm (1ft). Which of the following technologies should they utilize to meet these requirements?
###  1.Bluetooth2.NFC3.Wi-Fi4.RFID
#### Radio-frequency identification (RFID) uses electromagnetic fields to automatically identify and track tags attached to objects. The warehouse could utilize RFID to allow for the accurate scanning of items using radio frequency tracking tags and sending data of up to 2 KB to a sensor at rapid speeds. Near-Field Communication (NFC) is a set of communication protocols for communication between two electronic devices over a distance of 4 cm or less. This is used for train IC.
## Q3; In the context of Virtual Extensible Local Area Network (VXLAN), what is the purpose of the VXLAN Network Identifier (VNI)?
### 1.It is used to uniquely identify each VXLAN tunnel endpoint. 2.It is used to differentiate between different VXLAN overlay networks.3.It is used to authenticate VXLAN packets to ensure security.4.It is used to designate the source and destination IP addresses for VXLAN traffic.
#### The VXLAN Network Identifier (VNI) is a 24-bit identifier that helps differentiate between different VXLAN overlay networks. Each VXLAN segment or overlay network typically has a unique VNI assigned to it, allowing VXLAN endpoints to correctly identify and route traffic within the appropriate overlay network. The other options do not accurately describe the purpose of the VNI in VXLAN. For support or reporting issues, include Question ID: 65e905b593b8d475a949020c in your ticket. Thank you.
# April 15th
## Q1Which of the following is used to efficiently distribute power to racks of computer and networking equipment?
### 1.PDU 2.Generator 3.UPS 4.HVAC
####  A power distribution unit (PDU) is a device fitted with multiple outputs designed to distribute electric power, especially to racks of computers and networking equipment located within a data center. PDUs use and distribute the available amperage more efficiently, allowing your equipment to receive the best available power to maintain operation. An uninterruptible power supply or uninterruptible power source (UPS) is an electrical apparatus that provides emergency power to a load when the input power source or mains power fails. A generator is a device that converts motive power into electrical power for use in an external circuit. Generators can be powered by diesel, gasoline, or propane. Heating Ventilation and Air Conditioning (HVAC) units are responsible for maintaining the proper temperature and humidity within a datacenter
## Q2You are connecting a new IPv6 device to your network, but your routers only support IPv4 protocols. Which of the following IP addressing solutions would solve this challenge?
### 1.APIPA 2.Private 3.Classless 4.Teredo tunneling
#### Teredo is a transition technology that gives full IPv6 connectivity for IPv6-capable hosts that are on the IPv4 Internet but have no native connection to an IPv6 network. A private IP address is an IP address reserved for internal use behind a router or other Network Address Translation (NAT) devices, apart from the public. Private IP addresses provide an entirely separate set of addresses that still allow access to a network without taking up a public IP address space. Automatic Private IP Addressing (APIPA) is a feature in operating systems (such as Windows) that enables computers to automatically self-configure an IP address and subnet mask when their DHCP server isn't reachable. Classless IP addressing solutions allow for the use of subnets that are smaller than the classful subnets associated with Class A, Class B, or Class C networks.
## Q3Which of the following provides accounting, authorization, and authentication via a centralized privileged database, as well as challenge/response and password encryption?
### 1.ISAKMP 2.TACACS+ 3.Network access control 4.Multi-factor authentication
### TACACS+(Terminal Access Controller Access-Control System Plus) is a AAA (accounting, authorization, and authentication) protocol to provide AAA services for access to routers, network access points, and other networking devices. TACACS+ is a remote authentication protocol, which allows a remote access server to communicate with an authentication server to validate user access onto the network. TACACS+ allows a client to accept a username and password, and pass a query to a TACACS+ authentication server. RADIUS encypts password. TACACS+ is encrypt packet of text. **TACACS+** = AAA、ネットワーク機器管理、中央管理、暗号化・**RADIUS** = AAA、ネットワークアクセス認証でよく使う、**MFA** = 認証要素を増やす方式**NAC** = 接続してよい端末かを制御**ISAKMP(Internet Security Association and Key Management Protocol)** = IPsec の鍵交換まわり
## Q4: Quinn is configuring a wireless network for a client in an area known for dense wireless traffic and strict regulatory oversight on channel usage. To ensure compliance and optimal performance, they focus on incorporating a feature of the 802.11h standard. What aspect of 802.11h should Quinn prioritize to meet these requirements?
### 1.Beamforming technology 2.Multiple Input Multiple Output (MIMO) technology 3.Fast Roaming capabilities 4.Transmit Power Control
####  Transmit Power Control (TPC) is an important feature of the 802.11h standard that allows devices to adjust their transmitting power levels. This capability is crucial in areas with dense wireless traffic and strict regulatory oversight, as it helps minimize interference with other devices by reducing power to the necessary level for communication. Beamforming technology improves signal directionality and strength between the transmitter and receiver, enhancing network performance. Multiple Input Multiple Output (MIMO) technology increases network capacity and efficiency by using multiple antennas to transmit and receive data. Fast Roaming capabilities allow devices to switch between access points quickly, improving mobility within the network. 802h -> DFS(Dynamic Frequency Selection) and TPC
## Q5: A network technician needs to connect two switches. The technician needs a link between them that is capable of handling 10 Gbps of throughput. Which of the following media would BEST meet this requirement?
### 1.Coax cable 2.Fiber optic cable 3.Cat 5e cable 4.Cat 3 cable
#### To achieve 10 Gbps, you should use Cat 6a, Cat 7, Cat 8, or a fiber optic cable. Since fiber optic was the only option listed here, it is the best answer. A Cat 5e can only operate up to 100 meters at 1 Gbps. A Cat 3 cable can only operate at 100 meters at 10 Mbps. A traditional ethernet coaxial cable network can only operate at 10 Mbps, but newer MoCA coaxial ethernet connections can reach speeds of up to 2.5 Gbps.
## Q6: Dion Training believes there may be a rogue device connected to their network. They have asked you to identify every host, server, and router currently connected to the network. Which of the following tools would allow you to identify which devices are currently connected to the network?
### 1.Port scanner 2.Protocol analyzer 3.NetFlow analyzer 4. IP scanner
#### An IP scanner is used to monitor a network's IP address space in real-time and identify any devices connected to the network. Essentially, the tool will send a ping to every IP on the network and then creates a report of which IP addresses sent a response. A NetFlow analyzer is used to perform monitoring, troubleshooting, inspection, interpretation, and synthesis of network traffic flow data. A port scanner is used to determine which ports and services are open and available for communication on a target system. A protocol analyzer is used to capture, monitor, and analyze data transmitted over a communication channel. rogue divice -> IP scanner. Protocol analyzer can't transmit divices that don't transmit. Yes, a rogue device is not limited to a malicious device. It generally refers to any unauthorized or unmanaged device connected to the network, including both intentionally malicious devices and harmless-looking personal devices connected without approval.
## Q7: What one of the following systems is commonly used to manage digital certificates, ensuring secure communication and authentication over a network?
### 1.Symmetric Key Encryption 2.TLS 3.PKI 4.2FA
#### Public Key Infrastructure (PKI) manages digital certificates, including their issuance, revocation, and verification, providing a framework for secure communication and authentication. Symmetric key encryption uses a single key for both encryption and decryption, which doesn't address the issues of authentication and certificate management. Transport Layer Security (TLS) provides a means for privacy for communications over the internet, but does not deal with managing digital certificates. While two-factor authentication (2FA) enhances security by requiring additional verification beyond passwords, it doesn't directly manage digital certificates. TLS is not TCP function.
## Q8;You have been asked to connect three 802.11a devices to an 802.11g access point configured with WEP. The devices are within 20 feet of the access point, but they still cannot associate with the access point. Which of the following is the MOST likely cause off the devices not associating with the WAP?
### 1.Interference 2.Mismatched encryption 3.Signal loss 4.Frequency mismatch
#### 802.11a operates in the 5 GHz band, while 802.11g operates in the 2.4 GHz band. Therefore, 802.11a devices will be unable to communicate with 802.11b or 802.11g access points. Wireless networks utilize three different frequency bands: 2.4 GHz, 5 GHz, and 6 GHz. The 2.4 GHz frequency band is used by 802.11b, 802.11g, and 802.11n. The 5 GHz frequency band is used by 802.11a, 802.11n, 802.11ac, and 802.11ax. The 6 GHz frequency band is used by Wi-Fi 6E under the 802.11ax standard. WPA is Wi-Fi Protected Access that is security of WiFi. WAP is nearly AP
- **802.11a** → **5GHz**
- **802.11b** → **2.4GHz**
- **802.11g** → **2.4GHz**
- **802.11n** → **2.4GHz / 5GHz**
- **802.11ac** → **5GHz**
- **802.11ax** → **2.4GHz / 5GHz / 6GHzの文脈も出る**
- **802.11h** → **DFS / TPC**
- **802.11i** → **WPA2**
- **802.11r** → **Fast Roaming**
- **802.11ac** → **5GHz、高速化**
- **802.11ax** → **Wi-Fi 6**
- **802.11be** → **さらに新しい世代**
- #### 2.4GHz
- b
- g
- n
- ax
- be
- #### 5GHz
- a
- n
- ac
- ax
- be
- #### 6GHz
- ax（Wi-Fi 6Eの文脈）
- be
- それ以降の新しい世代
## Q9; Dion Training wants to create a DNS record to enter DKIM or SPF information into the domain name system and help prevent spam coming from their domain. Which type of DNS record should be created?
### 1.PTR 2.SRV 3.SOA 4.TXT
#### The DNS text (TXT) record lets a domain administrator enter text into the Domain Name Systems. The TXT record was originally intended as a place for human-readable notes. However, now it is also possible to put some machine-readable data into TXT records. TXT records are a key component of several different email authentication methods (SPF(Sender Policy Framework送ってよいサーバーです), DKIM(DomainKeys Identified Mail証明書), and DMARC(Domain-based Message Authentication Reporting and Conformance)) that help an email server determine if a message is from a trusted source. A DNS service (SRV) record specifies a host and port for specific services such as voice over IP (VoIP), instant messaging, and others. A Start of Authority (SOA) resource record indicates which Domain Name Server (DNS) is the best source of information for the specified domain. PTR records are used for the Reverse DNS (Domain Name System) lookup. Using the IP address, you can get the associated domain/hostname. An A record should exist for every PTR record.
