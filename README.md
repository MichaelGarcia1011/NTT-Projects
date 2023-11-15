# NTT-Projects

Creating a small business network

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
### Add Windows workstation (Test internet connection)
Ping:
- LAN - 10.128.0.1 (Reponsed)
- WAN - 8.8.8.8 (Request timed out. Connection to be establish)
- DNS - google.com (Request could not find host. Connection to be establish)







