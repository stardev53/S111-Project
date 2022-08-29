『 𝘗𝘙𝘖𝘑𝘌𝘊𝘛 - 𝘚111 』

![alt text](https://i.imgur.com/EAyB6Rt.png)
   

➤ 𝘋𝘦𝘣𝘪𝘢𝘯 𝘉𝘢𝘴𝘦𝘥 𝘚𝘰𝘭𝘶𝘵𝘪𝘰𝘯 𝘸𝘪𝘭𝘭 𝘣𝘦 𝘰𝘯 𝘶𝘴-𝘸𝘦𝘴𝘵-2

➤ 𝘙𝘦𝘥 𝘏𝘢𝘵  𝘉𝘢𝘴𝘦𝘥 𝘚𝘰𝘭𝘶𝘵𝘪𝘰𝘯 𝘸𝘪𝘭𝘭 𝘣𝘦 𝘰𝘯 𝘶𝘴-𝘦𝘢𝘴𝘵-1
    
➤ 𝘋𝘦𝘣𝘪𝘢𝘯 𝘝𝘗𝘊: 172.31.0.0/24 / 𝘙𝘦𝘥 𝘏𝘢𝘵 𝘝𝘗𝘊: 10.0.0.0/24

➥ IPS Used in this Project:

  ➥ ENTA:
  
       ➥ VPC: 10.0.0.0/24
        ➥ control.enta.pt: PUBLIC IP: 3.81.180.164 PRIVATE: 10.0.0.82 (Router) 
        ➥ central.enta.pt: 10.0.60.101 (Server)
        ➥ www.enta.pt: 10.0.50.101 (DMZ)
        ➥ wazuh.enta.pt: 10.0.60.102 (WAZUH)
        ➥ sales.enta.pt: 10.0.60.103 (SALES:CLIENT)
        ➥ marketing.enta.pt: 10.0.60.104 (MARKETING:CLIENT)
 ➥ INOVA 
 
       ➥ VPC: 172.31.0.0/24 (Default VPC By AWS)
        ➥ control.inova.pt: PUBLIC IP: 52.42.171.25 PRIVATE: 172.31.35.185 (Router)
        ➥ central.inova.pt: 172.31.129.101 (Server)
        ➥ www.inova.pt: 172.31.128.101 (DMZ)
        ➥ wazuh.inova.pt: 172.31.129.102 (WAZUH)
        ➥ sales.inova.pt: 172.31.129.104 (SALES:CLIENT)
        ➥ marketing.inova.pt: 172.31.129.103 (MARKETING:CLIENT)

 ➥ Remote Client
       
        ➥ Public IP: 52.27.115.44


📋 Summary of the Project

☁️ AWS Side ⇃

➣ Started creating 1 VPC in each region (𝘶𝘴-𝘸𝘦𝘴𝘵-2 (ENTA Side) and 𝘶𝘴-𝘦𝘢𝘴𝘵-1(Inova Side)

  ➨ Created 6 Machines for Ubuntu Side:
  
     ➨ Control.inova.pt ( VPN | SUBCA | DNS | NAT | FW | Teleport )
     ➨ www.inova.pt ( FTP / HTTP / HTTPS / EFS ) 
     ➨ central.inova.pt ( NIS / NFS / SMTP / POP3 / IMAP / RAID 5 )
     ➨ wazuh.inova.pt (Wazuh and Raid 6)
     ➨ Sales/Marketing.inova.pt (Graphic Interface / NIS / NFS / Thunderbird / firefox )
   
  ➨ Created 6 Machines for Amazon-Linux Side:
  
     ➨ Control.enta.pt ( VPN | CA | DNS | NAT | FW )
     ➨ www.enta.pt ( FTP / HTTP / HTTPS / EFS ) 
     ➨ central.enta.pt ( RAID 5 )
     ➨ wazuh.enta.pt (Wazuh and Raid 6)
     ➨ Sales/Marketing.enta.pt (None)


🚩 Description 🚩

☁️ Ubuntu Side ⇃

➣ On Control.enta.pt (Router) starting by giving a domain name to the machine and updating system.

    ☛ After that did NAT (Configured IP Tables for Routing and Give Internet to Clients)
    ☛ Configured netplan for the second network interface (eth2)    
    ☛ installed easy-rsa.   
    ☛ Configured dns server, my dns ip is : 172.31.35.185 (All VM's in the network have this ip on NETPLAN)    
    ☛ Configured OpenVPN, the main server vpn is on control.enta.pt (Amazon Linux)   
    ☛ Teleport setup
  
➣ on central:

    ☛ Configured netplan for dns and internet acess
    ☛ started by chaning hostname domain;
    ☛ configured netplan, adding the dns ip server from control and  gateway.
    ☛ configured raid 5 , nis and nfs
    ☛ central is the nis, nfs and email server!
    ☛ Imported ca.crt to the Documents folder from each user (maria and miguel)
    ☛ Users are mounted in /var/homes
    
➣ on wazuh server:
 
    ☛ Installed and configured the wazuh and deployed all agents on network (soc2) and raid 6!

➣ on dmz:
 
    ☛ Configured netplan for dns and internet acess
    ☛ Configured Ngins with HTTPS 
    ☛ Installed FTP Server
    ☛ Configured EFS System from aws.
    
➣ on Clients(Marketing/Sales):
 
    ☛ Configured netplan for dns and internet acess
    ☛ Configured Nis and NFS clients;
    ☛ Installed a Graphic Interface;
    
    
☁️ Amazon-Linux Side ⇃

➣ on control.enta.pt started configuring hostnamectl for machine domain;
      
    ☛ Configured IP Tables for NAT
    ☛ Created a Certificate Authority Server, on inove it is subordinate!
    ☛ OpenVPN Setup, this is the main vpn server!
    ☛ Configured DNS Server for entire amazon-linux network
    
➣ central.enta.pt:
  
    ☛ Configured network-scripts folder to give internet acess and to give the dns ip server!
    ☛ Raid 5 Setup
    ☛ Nfs Server Setup
    
➣ on wazuh server:
  
    ☛ Configured network-scripts folder to give internet acess and to give the dns ip server!
    ☛ Installed and configured the wazuh and deployed all agents on network
    ☛ Nfs Server Setup
    ☛ Raid 6 Setup!

➣ Clients Marketing/Sales:
  
    ☛ Configured network-scripts folder to give internet acess and to give the dns ip server!
    ☛ Installed Nfs Client.

  
