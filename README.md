γ πππππππ - π111 γ

![alt text](https://i.imgur.com/EAyB6Rt.png)
   

β€ ππ¦π£πͺπ’π― ππ’π΄π¦π₯ ππ°π­πΆπ΅πͺπ°π― πΈπͺπ­π­ π£π¦ π°π― πΆπ΄-πΈπ¦π΄π΅-2

β€ ππ¦π₯ ππ’π΅  ππ’π΄π¦π₯ ππ°π­πΆπ΅πͺπ°π― πΈπͺπ­π­ π£π¦ π°π― πΆπ΄-π¦π’π΄π΅-1
    
β€ ππ¦π£πͺπ’π― πππ: 172.31.0.0/24 / ππ¦π₯ ππ’π΅ πππ: 10.0.0.0/24

β₯ IPS Used in this Project:

  β₯ ENTA:
  
       β₯ VPC: 10.0.0.0/24
        β₯ control.enta.pt: PUBLIC IP: 3.81.180.164 PRIVATE: 10.0.0.82 (Router) 
        β₯ central.enta.pt: 10.0.60.101 (Server)
        β₯ www.enta.pt: 10.0.50.101 (DMZ)
        β₯ wazuh.enta.pt: 10.0.60.102 (WAZUH)
        β₯ sales.enta.pt: 10.0.60.103 (SALES:CLIENT)
        β₯ marketing.enta.pt: 10.0.60.104 (MARKETING:CLIENT)
 β₯ INOVA 
 
       β₯ VPC: 172.31.0.0/24 (Default VPC By AWS)
        β₯ control.inova.pt: PUBLIC IP: 52.42.171.25 PRIVATE: 172.31.35.185 (Router)
        β₯ central.inova.pt: 172.31.129.101 (Server)
        β₯ www.inova.pt: 172.31.128.101 (DMZ)
        β₯ wazuh.inova.pt: 172.31.129.102 (WAZUH)
        β₯ sales.inova.pt: 172.31.129.104 (SALES:CLIENT)
        β₯ marketing.inova.pt: 172.31.129.103 (MARKETING:CLIENT)

 β₯ Remote Client
       
        β₯ Public IP: 52.27.115.44


π Summary of the Project

βοΈ AWS Side β

β£ Started creating 1 VPC in each region (πΆπ΄-πΈπ¦π΄π΅-2 (ENTA Side) and πΆπ΄-π¦π’π΄π΅-1(Inova Side)

  β¨ Created 6 Machines for Ubuntu Side:
  
     β¨ Control.inova.pt ( VPN | SUBCA | DNS | NAT | FW | Teleport )
     β¨ www.inova.pt ( FTP / HTTP / HTTPS / EFS ) 
     β¨ central.inova.pt ( NIS / NFS / SMTP / POP3 / IMAP / RAID 5 )
     β¨ wazuh.inova.pt (Wazuh and Raid 6)
     β¨ Sales/Marketing.inova.pt (Graphic Interface / NIS / NFS / Thunderbird / firefox )
   
  β¨ Created 6 Machines for Amazon-Linux Side:
  
     β¨ Control.enta.pt ( VPN | CA | DNS | NAT | FW )
     β¨ www.enta.pt ( FTP / HTTP / HTTPS / EFS ) 
     β¨ central.enta.pt ( RAID 5 )
     β¨ wazuh.enta.pt (Wazuh and Raid 6)
     β¨ Sales/Marketing.enta.pt (None)


π© Description π©

βοΈ Ubuntu Side β

β£ On Control.enta.pt (Router) starting by giving a domain name to the machine and updating system.

    β After that did NAT (Configured IP Tables for Routing and Give Internet to Clients)
    β Configured netplan for the second network interface (eth2)    
    β installed easy-rsa.   
    β Configured dns server, my dns ip is : 172.31.35.185 (All VM's in the network have this ip on NETPLAN)    
    β Configured OpenVPN, the main server vpn is on control.enta.pt (Amazon Linux)   
    β Teleport setup
  
β£ on central:

    β Configured netplan for dns and internet acess
    β started by chaning hostname domain;
    β configured netplan, adding the dns ip server from control and  gateway.
    β configured raid 5 , nis and nfs
    β central is the nis, nfs and email server!
    β Imported ca.crt to the Documents folder from each user (maria and miguel)
    β Users are mounted in /var/homes
    
β£ on wazuh server:
 
    β Installed and configured the wazuh and deployed all agents on network (soc2) and raid 6!

β£ on dmz:
 
    β Configured netplan for dns and internet acess
    β Configured Ngins with HTTPS 
    β Installed FTP Server
    β Configured EFS System from aws.
    
β£ on Clients(Marketing/Sales):
 
    β Configured netplan for dns and internet acess
    β Configured Nis and NFS clients;
    β Installed a Graphic Interface;
    
    
βοΈ Amazon-Linux Side β

β£ on control.enta.pt started configuring hostnamectl for machine domain;
      
    β Configured IP Tables for NAT
    β Created a Certificate Authority Server, on inove it is subordinate!
    β OpenVPN Setup, this is the main vpn server!
    β Configured DNS Server for entire amazon-linux network
    
β£ central.enta.pt:
  
    β Configured network-scripts folder to give internet acess and to give the dns ip server!
    β Raid 5 Setup
    β Nfs Server Setup
    
β£ on wazuh server:
  
    β Configured network-scripts folder to give internet acess and to give the dns ip server!
    β Installed and configured the wazuh and deployed all agents on network
    β Nfs Server Setup
    β Raid 6 Setup!

β£ Clients Marketing/Sales:
  
    β Configured network-scripts folder to give internet acess and to give the dns ip server!
    β Installed Nfs Client.

    
    
    
    
Summing up, im more familiarized with debain base destributions linux then red hat.
On Ubuntu evertying is done, working and running, on amazon-linux not everything is done,
did my best for the time i had to do this project.
The Configurations for each one of the computers is here, feel free to use!
  
