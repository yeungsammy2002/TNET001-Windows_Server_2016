# Section 03 - Domain Controller Acting as Router

Here are the steps to set up a static route on Windows Server 2016:

#### 1. Open the Command Prompt as an administrator

#### 2. Enter the following command to view your current routing table:
```
route print
```

#### 3. Identify the interface that connects to the LAN by looking at the network destination for the `0.0.0.0` route. It should list the IP address of the LAN interface.

#### 4. Determine the IP address of the router that connects to the WAN. You can obtain this information from the router's configuration settings.

#### 5. Enter the following command to add a route to the WAN network via the WAN NIC:
```
route add <WAN network> mask <netmask> <WAN NIC IP address> -p
```
For example, if the WAN network is `192.168.0.0/24`, the netmask is `255.255.255.0`, and the WAN NIC IP address is `192.168.1.1`, you would enter the following command:
```
route add 192.168.0.0 mask 255.255.255.0 192.168.1.1 -p
```

#### 6. Enter the following command to add a route to the LAN network via the LAN NIC:
```
route add <LAN network> mask <netmask> <LAN NIC IP address> -p
```
For example, if the LAN network is `10.0.0.0/24`, the netmask is `255.255.255.0`, and the LAN NIC IP address is `10.0.0.1`, you would enter the following command:
```
route add 10.0.0.0 mask 255.255.255.0 10.0.0.1 -p
```
Note that the `-p` flag is used to make the route permanent, so that it survives a reboot.

#### 7. Verify that the new routes have been added by entering the following command:
```
route print
```
You should see the two new routes listed in the routing table.

By setting up static routes in this way, you can ensure that traffic is correctly routed between the LAN and WAN networks, without the need for multiple default gateways on the same machine.

