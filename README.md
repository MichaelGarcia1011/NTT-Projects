# NTT-Projects

Creating a small business network

## Stage1 : Network Setup

## Step 1
In GNS3 - drag all network equipment into the project and connect all the devices
- FortiGate (Firewall)
- LAN Switch
- DMZ Switch
- Win10 workstation
  
![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/43e14d94-3eec-4197-9855-34a1a2b76fc4)


## Step 2
In FortiGate PuTTY - Configure the FortiGate Firewall
- Create Password
  
![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/bb0e8f11-500d-454f-8a82-3eafd1c0a6b1)

### Configure Firewall (LAN gateway & interface)
-   LAN gateway is 10.128.0.1/24
-   LAN interface is named port2
  
![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/71ab3e15-41eb-450d-b702-12b4b05fe47c)

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/4dfebb58-d9a4-4a05-8c0a-d61323892a1c)


### Configure DHCP server for LAN Interface
- DHCP set pool scope to 10.128.0.[100-199]. Boundary set as per project parameters.

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/f395aba3-358c-4384-bdf6-07cf3069945f)

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/8731ccb7-f000-40e6-b1ff-5f3bcbf00759)


## Step 3 
### Test Internet Connection on Win10 Workstation
Ping:
- LAN - 10.128.0.1 (Responsed)
- WAN - 8.8.8.8 (Request timed out. Connection to be establish)
- DNS - google.com (Request could not find host. Connection to be establish)


## Step 4
Connect to FortiGate Firewall (utilize GUI) from Win10 Workstation.
Web Browser: http://10.128.0.1/

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/26bb851d-1f42-432d-9011-97dd89f69d4d)



System adjustments:  
- Hostname & Timezone
- Set idle to 60 mins
- Enable auto file system check

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/6f4ae0c0-9ace-430a-86f4-6acd60964bd9)

System > Settings

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/b97d56db-2160-4c53-9347-8e9545df7923)

Backup all Configurations
- [admin > configuration > backup]
- Save backup
- Save in download folder on Win10 Workstation


## Step 5
### In Web Browser (FortiGate Firewall) - Configure Network Interface
- 10.128.0.0/24 as the LAN network
- 10.128.99.0/24 as the GUEST network
- 10.128.10.0/24 as the DMZ network
- [Network > Interface]

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/6bf2833a-a05d-4034-858b-4b655a4011dc)

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/6f039734-007c-4419-b765-87a1ca8d8474)

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/a02bea15-10e1-45a1-869e-377fe9296572)

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/e5e24311-fabb-4460-9691-652dc19f9d74)

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/bdd3b705-da18-4ed0-aac6-38125344e207)

- Enable DNS: System > Feature Visibility (Must enable for settings to appear in GUI) 
- Configure firewall system DNS: [Network > DNS]

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/4d414eac-86ea-4a29-a0d3-3c3c3fcecadb)

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/e8025ec3-50d0-4c05-8ad2-0cafc129f5a0)

Note: 8.8.8.8 (google) and 1.1.1.1 (cloudflare) are just well-known public DNS servers
Note: This tells the firewall to use this DNS servers for it's own DNS requests.

### Configure Network DNS
DNS server = same as interface IP
- [Network > DNS Servers]

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/8baf32a9-1aed-4423-bb46-0854059829bb)

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/bd968b02-6ea4-4c01-9876-af10646e6223)

### Configure Service Objects
- [Policy & Objects > Services]

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/44401d53-6700-4c00-bb90-890c0ae7fda4)

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/94c1efef-7874-439a-b0fd-b37df1f6ddf3)

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/e0686ff3-d8a8-463b-b824-5697194dee3a)

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/d1498ac2-4f65-45fc-8fe8-9b57f65f36f2)

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/0ff1f09f-9e09-4a5f-8064-b86ffd5c02c2)

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/f81f28e5-2a0a-4ffd-974b-016cb472ea92)

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/ae04841c-38f7-4392-87e3-07800323f29e)


# Stage2 : Domain Setup

## Step 1
In GNS3 - drag in a server (Win2012r2) and connect to established LAN switch

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/88e8e934-fad1-451c-9134-71e73b8965ee)


## Step 2: Set a static IP address
- ip address: 10.128.0.10
- subnet mask: 255.255.255.0
- default gateway: 10.128.0.1
- DNS primary: 127.0.0.1
- DNS alternative: 10.128.0.1

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/caf5c972-d286-4450-8168-16236d75a466)

## Step 3: Test LAN, WAN, and DNS network connectivity utilizing Ping.
- LAN - 10.128.0.1 (Response)
- WAN - 8.8.8.8 (Response)
- DNS - google.com (Response)

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/f3e8f195-b793-4489-9992-582556a8d873)


## Step 4: Configure NTP (Network Time Protocol)
- Set timezone and sync with the LAN interface IP on the firewall utilize: 10.128.0.1 

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/42caba05-3a25-40cf-83cf-ae2bbba1e665)


## Step 5: Change Hostname to dc (Domain Controller)

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/a211bd22-0a06-4e4c-b691-e633f2317f9a)

## Step 6: Install Active Directory
- Initial startup to Server, set and establish password
- Change computer name to dc (Local Server > Computer name hyperlink)

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/2630c78c-c36f-45c8-bc6a-2ff73e7e19f8)


- Validate connectivity by checking IP address, subnet mask, default gateway, & DNS primary utilizing ipconfig & IPv4 properties.

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/ed7abdd0-02ea-46e0-a46d-fa060f067ff8)

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/389bf3cb-5d87-43e0-acfd-44e9dfe0ae43)

## Step 7: Install Directory Services role
In Server Manager, Manage tab > Add Roles and Features

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/563cefbd-5d83-4f7c-a146-924bb6d4b24b)

- Installation Type (Keep the defaults)
- Server Selection (Keep the defaults)

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/660a63ac-f606-452c-a19c-3d7a70d8ee7a)














