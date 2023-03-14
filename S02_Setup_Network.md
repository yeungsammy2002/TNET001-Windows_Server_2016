# Section 02 - Setup Network

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
        local DHCP MAC: (2C:27:D7:2A:4B:AF)
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
      Switch --|> DomainController
      Client --|> Switch
```
