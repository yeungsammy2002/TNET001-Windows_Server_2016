# Section 02 - Setting Up Network

We're going to set up a network that ranged from `11.11.11.1` to `11.11.11.254` with a domain called `demo.com`.

Here is the basic set up diagram for our `demo.com` network with DNS configuration:
```mermaid
classDiagram
    class Router {
        WAN: IP from external DHCP
        LAN: (Configure manually)
        Router IP: (11.11.11.1 default gateway)
        Subnet Mask: (255.255.255.0)
        local DHCP Server: (11.11.11.2)
        local DHCP MAC: (60:32:B1:54:10:9E)
    }

    class DomainController{
        DNS Server
        NIC DNS Configuration:
        NIC IP: 11.11.11.2
        Subnet Mask: 255.255.255.0
        default gateway: 11.11.11.1
        Preferred DNS: 127.0.0.1
        DCHP Scope Configuration(local)
        003 Router: (11.11.11.1)
        006 DNS Server: (11.11.11.2)
        015 DNS Domain Name: (demo.com)
    }

    class Client{
        Domain User
        DNS Configuration(from local DHCP)
    }

    Internet --|> Router
    Router --|> Switch
    Switch <|-- DomainController
    Client --|> Switch
```



## Setting up Router DNS Configuration

- #### 1. Access Router Configuration Interface 
We need to set up **LAN** part of the router including IP address, subnet mask, default gateway. To do this, we need to access the router configuration interface through browser. By default, the IP address of ***ASUS RT-AC68U*** is `192.168.1.1`. So open the ***Edge*** browser, enter `192.168.1.1`.

- #### 2. Set Up Local Router IP & Subnet Mask
On the router interface, click **"LAN"**, then we need to set up the router IP address and subnet mask. In our case:
```
router IP:       11.11.11.1          // default gateway
subnet mask:     255.255.255.0
```

- #### 3. Turn Off Router DHCP 
On the router interface > **LAN** > **DHCP** section, turn off **"Enable DHCP Server"** option.

- #### 4. Setup External DHCP
We're going to set the IP address of this server to `11.11.11.2` and find out the MAC address of this server so that we can tell the router where is the external DHCP server.

To do this, we need to go back to the desktop of this server. Open the command prompt to get the MAC address of this server by running `getmac` command:
```
C:\Users\Administrator>getmac

Physical Address    Transport Name
=================== ==========================================================
60-32-B1-54-10-9E   \Device\Tcpip_{907F023E-2264-4F4D-906C-11E15C8B4657}
```
Back to the ***Edge*** browser window. On the router interface > **LAN** > **DHCP** section, enter both the DHCP server MAC address and IP address in the **manual DHCP server list**:
```
Mac address             IP address
60:32:B1:54:10:9E       11.11.11.2
```



## Setting Up Server DNS Configuration & Promoting Server to Domain Controller

- #### 1. Setup Server IP Address
Back to this server's desktop, open **"Server Manager"** window. Click the ***value*** of the **"Ethernet"** field ->

right-click **"Ethernet"** icon (on **"Network Connections"** window) -> click **"Properties"** ->

click **"Internet Protocol Version 4(TCP/IPv4)"** (on **"Ethernet Properties"** window) -> **"Properties"** button ->

Complete the DNS configuration (on **"Internet Protocol Version 4 (TCP/IPv4) Properties"** window) as follow:
```
- Use the following IP address:
    IP address:                 11.11.11.2
    Subnet mask:                255.255.255.0
    Default gateway:            11.11.11.1

-Use the following DNS server addresses:
    Preferred DNS server:       127.0.0.1
    Alternative DNS server:     [empty]
```

- #### 2. Add "Active Directory Domain Service" Role
So far, you cannot connect to the internet yet because this server cannot resolve its DNS server. So you need to add **"Active Directory Domain Service" (AD DS)** role to this server at first. Once this server added **AD DS** role, you could promote this to a domain controller and add **"DNS server"** role to this.

To add **"Active Directory Domain Service"** role, you need to open the **"Server Manager"** at first.

Click **"Manage"** (top right menu bar on **"Server Manager"** window) -> **"Add Roles and Features"** ->

-> **"Next"** (on **"Before you Begin"** tab of **"Add Roles and Features Wizard"** window) ->

-> **"Role-based or feature-basesd installation"** (**"Installation Type"** tab) ->

-> **"Select a server from the server pool"** (**"Server Selection"** tab) ->

-> check **"Active Directory Domain Services" checkbox** (**"Server Roles"** tab) -> 

-> leave remaining things as default and continue through the prompt until the end

- #### 3. Promote Server to Domain Controller & Add "DNS Server" Role
Back to the **"Server Manager"** window, **"notification flag"** icon appeared on the top right menu bar, click on the icon -> **"Promote the server to a domain controller"** ->

**Add a new forest** and enter `demo.com` in the **"Root domain name:"** field (on **"Deployment Configuration"** tab of **"Active Directory Domain Services Configuration Wizard"** window) ->

-> make sure the **"Domain Name System (DNS) server"** and **"Global Catalog (GC)"** checkboxes are checked and enter **"DSRM password"** (on **"Domain Controller Options"** tab) ->

-> make sure the **"Create DNS delegation"** checkbox ***uncheck*** (on **"DNS Options"** tab) ->

-> leave **"The NetBIOS domain name:"** field as default `DEMO` (on **"Additional Options"** tab) ->

-> leave remaining things as default and continue through prompts until the end

#The **"Global Catalog"** option means that the server will list all ***Active Directory objects***

#The **"DSRM password"** allows an administrator to **take an instance of AD offline** for maintenance or troubleshooting. This is not commonly used, but you have to keep the password around just in case.

#Leaving **"Create DNS delegation"** uncheck so that people from outside will **NOT** be able to resolve **local DNS names** on your **local DNS server**, names like `demo.com`. This is fine because we don't want people on the Internet to be able to access our server.

- #### 4. NetBIOS Appeared on Login Cover Page
Once the server restart and you'll see the login cover page, you should see the **NetBIOS** name of our domain `DEMO` proceeds the user account we are logging into. In this case, `DEMO\Administrator`, this is in the format of `[domain name]\[domain user name]`
    
If you had multiple domains, we could specify a different domain by typing in the `[domain name]\[domain user name]` on the login cover page.

Once you logged in, the first thing you're notice is a new role - **AD DS** and **DNS** in the **"Server Manager" window**, and the serve should be able to connect to the internet now.



## Adding DHCP Role to Server and Configuring DHCP Server
In order to assign IP addresses to client computers within `demo.com` network, you need to add **DHCP** role to the server by using **"Server Manager"**.

After the role is added, you need to open **"DHCP" Microsoft Management Console (MMC)**. To do this, open **"Server Manager"**.

On the **"Server Manager"** window, click **"Tools"** (top right menu bar on **"Server Manager"** window) -> **"DHCP"**. The **DHCP MMC** should be appeared.

On the **DHCP MMC**, expand `demodc.demo.com`, you should something like this:
```
DHCP
    demodc.demo.com
        > IPv4
        > IPv6
```

Click **"IPv4"** -> right-click **"IPv4"** -> **"New Scope..."**. A **"New Scope Wizard"** window should be appeared.

On the window, set up the **"Scope Name"** as follow:
```
Name:           IPv4 Scope
Description:    11.11.11.1 - 254
```

Set up the **"IP Address Range"** as follow:
```
Configuration settings for DHCP Server
    Enter the range of addresses that the scope distributes.
        Start IP address:   11.11.11.1
        End IP address:     11.11.11.254

Configuration settings that propagate to DHCP Client
        Length:             24              // auto filled
        Subnet mask:        255.255.255.0
```

Set up the **"Add Exclusions and Delay"** as follow:
```
Start IP address:       End IP address:
11.11.11.1              11.11.11.20
```

Leave the **"Lease Duration"** as default and that is **8 days**.

On the **"Configure DHCP Options"** window, select **"No, I will configure these options later"** option. Then continue through the prompt until the end.



## Configuring DHCP Scope
Back to the **DHCP MMC**, on the ***left pane***, expand `demodc.demo.com` -> expand **"IPv4"** -> expand **"Scope[11.11.11.0] IPv4 Scope"** -> right-click **"Scope Options"** -> **"Configure Options..."**. A **"Scope Options"** window should be appeared.

On this window, check the checkboxes and fill the data as follow:
```
[v] 003 Router                  IP address:     11.11.11.1
...
[v] 006 DNS Servers             IP address:     11.11.11.2
...
[v] 015 DNS Domain Name         String value:   demo.com
```

Once **DHCP "Scope Options"** are configured, the DHCP server should be able to assign IP addresses to all the client computers that connected to the `demo.com` domain network.