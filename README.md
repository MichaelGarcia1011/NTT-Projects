# Project: Creating a Small Business Network

## STAGE 1 : NETWORK SETUP

## Step 1: Drag Network Equipment into the Project.
In GNS3 - Drag and connect all devices to the established WAN Cloud & WAN Switch.
- FortiGate (Firewall)
- LAN Switch
- DMZ Switch
- Win10 Workstation
  
![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/caad0d8f-c242-487a-b55f-9378f15e5568)


## Step 2: Configure the LAN Network.
In FortiGate PuTTY - Configure the FortiGate Firewall
- Create Password
  
![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/bb0e8f11-500d-454f-8a82-3eafd1c0a6b1)


### Configure Firewall (LAN gateway & interface)
-   LAN gateway is 10.128.0.1/24
-   LAN interface is named port2
  
![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/71ab3e15-41eb-450d-b702-12b4b05fe47c)

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/1de5da18-23ab-4fcc-b019-a63840edf96c)


Verify the configuration: [show sys int port2]

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/4dfebb58-d9a4-4a05-8c0a-d61323892a1c)


### Configure DHCP server for LAN Interface
- Enable the DHCP sever on the LAN interface.
- The firewall will perform DHCP services for devices on the LAN network.
- Set the DHCP pool scope to 10.128.0.(100-199). Boundary set as per project parameters.

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/f395aba3-358c-4384-bdf6-07cf3069945f)

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/fc5e4f2d-5ec4-41b3-815b-a0360459bcaa)


Verify the configuration: [show sys dhcp server 1]

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/8731ccb7-f000-40e6-b1ff-5f3bcbf00759)


## Step 3: Add a Win10 Workstation
- Start the Win10 workstation in GNS3, and then double click it to connect through VNC.
- The first time you start Win10 it will take a minute or two to setup.
- Click-and-hold the background image and drag up to show the login prompt.

### Verify the Win10 workstation has leased a DHCP address from the LAN network.
- Valid IP Range: 10.128.0.(100-199)/24
- Gateway: 10.128.0.1
- DHCP Server: 10.128.0.1

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/37a443d4-592a-4518-9180-07dd1fcdf1eb)


### Test Internet Connection on Win10 Workstation
Ping:
- LAN - 10.128.0.1 (Responsed)
- WAN - 8.8.8.8 (Request timed out. Connection to be establish)
- DNS - google.com (Request could not find host. Connection to be establish)

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/df954cec-74a9-4fa1-a390-bbb9afa368ea)


## Step 4: Connect to FortiGate Firewall GUI
From Win10 Workstation, Open Web Browser and enter http://10.128.0.1/

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/26bb851d-1f42-432d-9011-97dd89f69d4d)


### System adjustments:  
System > Settings
- Hostname & Timezone
- Enable Local NTP Server
- List on Interface: port2 & port4
- Set idle to 60 mins
- Enable auto file system check

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/6f4ae0c0-9ace-430a-86f4-6acd60964bd9)

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/82aebba5-4a2f-47b8-a378-322d82fe8ab8)

### Backup all Configurations
- Click Admin (Upper Right-hand Corner) > Configuration > Backup
- Save backup in download folder on Win10 Workstation
- Reboot Firewall

## Step 5: Complete the Network Setup
Open the Web Browser on the Win10 Workstation and connect to the firewall GUI (FortiGate Firewall) - http://10.128.0.1/ 

### Configure Network Interface
- 10.128.0.0/24 as the LAN network
- 10.128.99.0/24 as the GUEST network
- 10.128.10.0/24 as the DMZ network
- Network > Interface

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
- Network > DNS Servers

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/8baf32a9-1aed-4423-bb46-0854059829bb)

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/bd968b02-6ea4-4c01-9876-af10646e6223)

### Configure Service Objects
- Policy & Objects > Services

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/44401d53-6700-4c00-bb90-890c0ae7fda4)

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/94c1efef-7874-439a-b0fd-b37df1f6ddf3)

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/e0686ff3-d8a8-463b-b824-5697194dee3a)

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/d1498ac2-4f65-45fc-8fe8-9b57f65f36f2)

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/0ff1f09f-9e09-4a5f-8064-b86ffd5c02c2)

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/f81f28e5-2a0a-4ffd-974b-016cb472ea92)

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/ae04841c-38f7-4392-87e3-07800323f29e)


# STAGE 2 : DOMAIN SETUP

## Step 1: Prepare a Win2012r2 Server
In GNS3 - drag in a server (Win2012r2) and connect to established LAN switch

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/88e8e934-fad1-451c-9134-71e73b8965ee)


## Step 2: Set a static IP address
- IP Address: 10.128.0.10
- Subnet Mask: 255.255.255.0
- Default Gateway: 10.128.0.1
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
- Server Selection (Keep the defaults) - select Server in server pool.

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/660a63ac-f606-452c-a19c-3d7a70d8ee7a)


- Server Roles - check mark Active Directory Domain Services.
- Features (Keep the defaults)

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/85c52b6d-4574-44ff-a0a7-2c00c3dc28bd)


- Confirmation - click install (Active Directory binaries will be installed)
- After installation, click the yellow flag for further configurations to create a domain controller.

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/6ecedb51-e29f-4ae9-bf8b-0c041625f508)


- Click the "Promote this server to a domain controller" link.
- Select: "Add a new forest" and then type the domain name that you want, then click Next.
- The Active Directory Domain Services Configuration Wizard window will appear.

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/344f792f-b053-4bde-83da-69386ae61fa0)


### Domain Controller screen:
- Select the Forest functional and Domain functional level (Keep defaults)
- Set a password

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/c31f039a-3957-4fb3-b719-bbad129a0188)


- DNS options (Keep defaults)
- Additional options (Keep defaults)
- Paths (Keep defaults)
- Review options (Keep defaults)
- Prerequisites Check: Review and Install

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/f22e5eb2-2d5a-44b0-aead-49b95dc5ff9b)


## Step 8: Create new Active Directory users
Server Manager > Tools > Active Directory Users and Computers

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/3d637206-a1a9-449f-bdfe-daa2a4f2a7cf)

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/64d83a96-162f-4130-97ba-87bfec4fdc17)

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/40c72d6b-e243-48c8-b198-94ce37c01b62)

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/2612d27a-aa0b-4e3c-8b3f-d8942c580354)


- Add new admin to the admin group

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/02780a9b-3a99-42ab-a70e-ed6bdb78d646)

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/f13ac3ac-3a40-4d2e-b38d-7b1d8496452f)

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/dcda4017-d551-4d5f-a8d8-d83b100cdad5)


## Step 9: Prepare Win10 workstation to join the domain
- Change the hostname to win10, then reboot.
- Change the primary DNS server to the IP for the DC.
- Set NTP to sync with dc.widgets.localdomain

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/8cd89771-87fc-4291-a464-9da2e42d49e3)

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/faa67ff1-24b1-407a-b1e8-4b66690c78d8)

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/6c367464-4abf-4da2-9a93-afcda1744447)

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/69758ea0-7d74-4d01-ae47-d776ca1215ba)


## Step 10: Join Win10 to the widgets.localdomain domain

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/4e2a342d-598e-4ce0-9ba2-1ef91f38f20a)


### Join a Computer to a Domain (Microsoft Directions)
- On the Desktop, click the Start button, type Control Panel, and then press ENTER.
- Navigate to System and Security, and then click System.
- Under Computer name, domain, and workgroup settings, click Change settings.
- Under the Computer Name tab, click Change.
- Under Member of, click Domain, type the name of the domain that you wish this computer to join, and then click OK.
- Click OK in the Computer Name/Domain Changes dialog box, and then restart the computer.

### Join a Server to a Domain (Microsoft Directions)
- On the Desktop, click the Start button, type Control Panel, and then press ENTER.
- Navigate to System and Security, and then click System.
- Under Related settings, click Rename this PC (advanced).
- Under the Computer Name tab, click Change.
- Under Member of, click Domain, type the name of the domain that you wish this server to join, and then click OK.
- Click OK in the Computer Name/Domain Changes dialog box, and then restart the server.

## Step 11: Set the desktop background with GPO

- Edit the Default Domain Policy
- On the dc, login and open the Group Policy Management Console, edit the Default Domain Policy.

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/f38938c9-3139-4d94-8fb0-72a10b859b92)

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/3f3e32f3-229f-4f5e-8227-9fb69e9aebd3)


- Logout of win10, and then log back in: Background should be updated.
- You can use gpupdate and gpresult to troubleshoot GPO issues.

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/9c6e3f6e-68d5-4e20-85d5-1f6ab13c207c)


# STAGE 3: IIS Setup

## Step 1: Prepare a Win2012r2 server
In GNS3 - drag in a server (Win2012r2) into project and connect to established LAN switch
- Static IP: 10.128.0.80
- Subnet mask: 255.255.255.0
- Default Gateway: 10.128.0.1
- Set dc IP as primary DNS (10.128.0.10)
- Firewall DMZ IP as secondary DNS (10.128.0.1)
- Sync NTP with dc.widgets.localdomain
- When changed, join to the widgets domain

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/09ae8ff6-d64f-4bf0-8529-05202660bd19)

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/d9377790-4fe2-42b6-a26d-82cb278fbb05)

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/decdca86-2f2d-49cf-9006-040e18287d97)


## Step 2: Install the IIS Role - Add Roles and Features Wizard in Server Manager
- On Installation Type page, select Role-based or feature-based installation to configure a single server. Click NEXT.

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/58db9317-20a1-41ed-84f6-fca2ca5067bf)


- On Server Selection page, select Select a server from the server pool, and then select a server. Click NEXT.

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/b9673632-83e2-47a4-8d56-4d7a3f8303f4)


- On the Server Roles page, select Web Server (IIS).

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/9703f479-fdea-4dff-8913-1597d413832b)


- In the Add Roles and Features page, click Add Features to install the IIS Management Console. Check mark Include Management tools.
- Then click NEXT on the Server Roles page.

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/6f532fd5-51ce-4d67-8b4c-3fa3bffb494a)


- On Features page, keep defaults. Select additional features if needed then click NEXT.

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/be447250-bb03-48c6-b6c5-0f59b185f80b)


- On Web Server Role (IIS) page, click NEXT.
- On Role Services page, keep defaults. Select additional features if needed then click NEXT.

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/1c07be42-cf84-4ca2-9c74-ef795d72a320)


- On Confirmation page, click INSTALL.

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/409cc6ce-7ab7-46bf-b20d-b6b18603369d)


- After installation is successful, a Results page will appear.

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/2f6abf05-988f-4ad7-a57b-ff247ec7d3b6)


## Step 3: Confirm that the Web server works by opening a Web browser. 
- Enter http://localhost in the web browser.

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/c2a3b64b-1ddd-42be-a3d4-1aa7ab7bd8a1)


## Step 4: Trust the Website.
- On Web Browser, click the gear symbol (upper right-hand corner), select Internet Options.

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/552d3250-ab08-45ac-9dea-2adfff497ca2)


- On Internet Options window, select the security tab > Trusted sites > Sites
- On Trusted Sites window, [http://localhost] should be in the "Add this website to the zone:" box, then click ADD, then OK. 

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/9393a57b-f690-4856-8394-b920487a2331)


## Step 5: Setup a test webpage on IIS
Create the HTML file
- Open notepad and add the following:

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/6fa2bf01-f216-4a84-a5d8-d507461edeaa)


- Save the file to your documents folder as: test.html
- Copy the file from your documents folder to: c:\inetpub\wwwroot\test.html
- Test in local browser on IIS: http://localhost/test.html

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/570cb217-0671-4264-add2-0d0024786818)

- Then test from the Win10 Workstation: http://iis.widgets.localdomain/test.html


# STAGE 4 : LAMP Setup

## Step 1: Prepare the Ubuntu Server
- In GNS3, drag QUME VM Ubuntu in project and connect to established DMZ switch. 

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/e9790003-8649-402b-b6fe-f13bdbbf508a)


### Configure network settings
- IP Address: 10.128.10.80
- netmask: 255.255.255.0
- gateway: 10.128.0.1
- DNS: 10.128.0.10, 10.128.10.1

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/813d3a4f-6aa3-4ffd-865d-0dff5bad8491)


## Step 2: Update Host file
- Open Terminal, change to root [sudo -i] > enter password.
- ### Edit Host file [nano /etc/hosts]
  - 127.0.0.1 localhost.localdomain localhost
  - 10.128.10.80 www.widgets.localdomain www
    
![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/6b8ad9ad-893d-475e-81f6-74ade0d588fc)

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/59816a1a-6a8f-4062-b319-9b36fb0cf8d0)


- ### Set hostname with hostnamectl
  - hostnamectl set-hostname www
  - hostnamectl

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/37bef485-c45f-4024-a1ff-167594934773)


## Step 3: Update packages on the Server
- [apt update -y]
- [apt upgrade -y]
- [apt dist-upgrade -y]
- [apt autoremove -y]
- [apt autoclean -y]
- [systemctl reboot]

NOTE: *Upgrades will take a few hours.

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/20183d1e-71a7-4d67-8924-88113d99a065)


# STAGE 5 : FTP Setup

## Step 1: Prepare a Win2012r2 server
In GNS3 - Drag a server into project and rename to FTP host.
- Static IP: 10.128.10.21
- Subnet mask: 255.255.255.0
- Default Gateway: 10.128.10.1
- Set dc IP as primary DNS (10.128.0.10)
- Firewall DMZ IP as secondary DNS (10.128.10.1)
- Sync NTP with dc.widgets.localdomain
- Change the hostname to ftp.


![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/45766880-722a-4d77-9df1-d346cf399183)


![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/623fd3eb-6beb-43ea-a8bb-b4298654536d)


![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/6aa9baa7-dfd8-41ff-985e-965b637c9718)


![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/727008ce-bad2-4f6e-8aea-5145fb313d61)


![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/123803c8-b61c-40c7-9f2d-00663c10eb1b)


## Step 2: Install FTP Services

### In Server Manager, Manage tab > Add Roles and Features

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/563cefbd-5d83-4f7c-a146-924bb6d4b24b)


- Installation Type (Keep the defaults)
- Server Selection (Keep the defaults) - select Server in server pool.

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/660a63ac-f606-452c-a19c-3d7a70d8ee7a)


- Server Roles - check mark Active Directory Domain Services, DNS Server, and File & Storage Services.
- Select the IIS Webserver (Add Feature).

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/bafcd1db-3eb0-4aff-915e-8fa157acb38e)


- Features (Keep defaults), NEXT.

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/93a7dd24-768c-47b1-b901-e4d589e1b108)


- Web Server Role (IIS), NEXT.
- Role Services, check mark FTP Server, then FTP service and FTP Extensibility.
- Keep all deafaults, NEXT. 

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/aebc661b-f541-4b47-8135-002805bae37e)


- Confirmation, select NEXT, Warning message appears to restart after installation, YES.
- Results, select CLOSE when installation is complete and server will restart.

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/f2b3c18b-1f73-4a84-9bc3-c7c1b7da0ec1)

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/54ed3135-700e-4f32-9fb7-41937a46de60)


### After Installation of FTP Services
In the FTP Server, Service Manager > Tools > Internet Information Services (IIS) Manager > SRV-8 Home (left column). 

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/159605c3-f1e4-40b2-bbe2-ec013d15acd4)


- Create a FTP folder in the local disk (C:), 

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/986fb763-a77f-4485-94bc-90548555b893)

- Add a FTP site.

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/62438686-8b77-4c0c-89e7-2db5ff7e4701)

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/b46cb4f7-e1f6-4fef-8891-f28212ed47ef)

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/b823cd4d-1d11-4ae5-bb69-f83847341c54)


- Add the Users/Groups, given read and/or write permissions. 

![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/555d0e30-6546-4dc0-af7e-3287c7ce4cba)


- After adding Users/Groups, Open Browser and test the website at: ftp://ftp.widgets.localdomain/
- A window message box will appear requiring username and password. Enter the website should appear as below.
  
![image](https://github.com/MichaelGarcia1011/NTT-Projects/assets/150825876/a85ee165-64a8-45c2-bccd-a7089f1b3de4)




























