# Section 01 - Setup Window Server 2016 and Setup a Network

Here is the basic set up diagram for our demo network:
```mermaid
classDiagram
    class Router {
        WAN: IP from external DHCP
        LAN: (Configure manually)
        Router IP: (11.11.11.1 default gateway)
        Subnet Mask: (255.255.255.0)
        local DHCP Server: (11.11.11.2)
        local DHCP MAC: (2C:27:D7:2A:4B:AF)
    }

    class DomainController{
        DNS Server
        NIC DNS Configuration:
        NIC IP: 11.11.11.2
        Subnet Mask: 255.255.255.0
        default gateway: 11.11.11.1
        Preferred DNS: 127.0.0.1
        DCHP Scope(local)
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
      Switch --|> DomainController
      Client --|> Switch
```



## Basic Setup of Router
Before installing Windows Server 2016 on a server, you need to set up a router that is used to connect to internet. This router is also needed to be set up correct DNS configuration for LAN.


