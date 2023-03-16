# Windows Server 2016 - part 1




# Overview of Windows Server 2016
We're going to cover various key components that a commonly used by system administrators who manage ***Windows Server 2016*** server.

All this informations provided by ***itflee.com***. **Youtube link** for the full tutorial: **https://www.youtube.com/playlist?list=PLYogJ_kxL1wTesq-vNxEc8tjDOHvszeWf**



## Server Manager
The primary way that you manage your server the program called **"Server Manager"**. By default **"Server Manager"** will launch when the operating system starts. ***Server Manager*** allows you to manage your local server as well as other servers on your local network. From here, you can manage your ***computer name***, ***IP address***, ***firewall settings***, ***Windows updates***, the **advanced services** and much more.

In the **"Server Manager" window**, on the left pane, there are 4 tabs - **"DashBoard"**, **"Local Server"**, **"All Servers"** and **"File and Storage Services"**. The first 3 items related to the server or remote services. The forth **"File and Storage Services"** is the ***server role***, this is installed by default. **Whenever you install a new server role, they will appeared in this *left pane***.


- ### Dashboard
**"Dashboard"** is the quick overview server, and allows you configure the server quickly. If there are any issues with the local server, or the remote servers, such as server that failed to started, you will see them on the screen.

To see errors on the remote servers, you need to first add them as the ***remotely managed server***. Errors on the remote servers will be shown on the **"All Servers" section** on the ***Dashboard***


- ### Local Server
**"Local Server"** will give you detail information about the server you're currently logged on to. If you needed to change anything from the ***computer name***, ***domain membership***, ***firewall***, ***network settings***, etc... This is the place to do it.


- ### All Servers
***"All Servers"*** allows you to do the same advance services and other informations, but you cannot change the computer properties such as computer name, network information and firewall settings.


- ### File and Storage Services
**"File and Storage Services"** is a server role includes technologies that help you setup and one or more file servers, which are servers that **provide central location on your network where you can storage files and share them with other users**.



## Roles and Features
There are **two key terms** you must know in order to successfully work on ***Windows Server 2016***.

A ***server role*** is a set of software programs that allow a server to provide a specific service to its network. An example of role will be adding a **"DHCP" role** to a server, this will allow the server to act as a **"DHCP" server**.

***Features*** are individual software programs that are sometimes required to install by ***roles*** although it can be independently installed without role as well. We can add or remove roles and features by selecting the **"Manage" button** on the top right hand corner of the **"Server Manager" window**, and selecting either **"Add Roles and Features"** or **"Remove Roles and Features"**. The window for adding and removing roles are nearly identical, one allowing you to check checkboxes for roles, and the other allowing you to uncheck role checkboxes.


- ### Add Roles and Features
To add ***roles*** and ***features***, you have to click on **"Manage"** -> **"Add Roles and Features"**. Then a **"Add Roles and Features Wizard" window** popped up. You will presented with the **"Before you begin" tab**, this tab have no functionality and simply informational. We recommend you read over and check the **"Skip this page by default" checkbox** before you press **"Next"**.

On the **"Installation Type" tab**, the first option **"Role-based or feature-based installation"** is the most common, and is for installing **role and features** on a **single server**. The second option **"Remote Desktop Service installation"** is for installing roles onto a ***virtual machine***. Usually we should choose the ***first option***, then click **"Next"**.

On the **"Server Selection" tab**, if you've added remote servers to manage, then they will be listed on **"Server Pool"** on the ***main pane***. You can also choose to install the roles on the ***virtual harddisk***. Unless you're using **Hyper-V**, you likely won't use the second option. Leave it as default and click **"Next"**.

On the **"Server Roles" tab**, you will choose any of the ***roles*** you would like to add to the server. If you only want to install ***features***, you don't have to check any of these checkboxes. For example, check the **"Fax Server" checkbox**. You will get a **popped up window** saying that you need to add addition required features in order to install this role, check **"Add Features"**. Then back to the tab and click **"Next"**.

The **"Features" tab** looks very similar to the **"Server Roles" tab**, if you're not selected any ***role*** to install, you will not be able to progress past the screen. It is important for you to know that you don't have to install any ***server roles***. But you must at least install ***features*** in order to complete this wizard. Click on **"Next"** to continue.

Then it will prompt to the ***new fax server role*** we're installing on the **"Fax Server" tab**. Generally, when you add a new server role, you will have some type of informational tabs added to the wizard. Click on **"Next"** and you'll the server's **"Role Services" tab**, you can check ***additional services checkboxes*** if you would like. Click on **"Next"**.

We are bought to the **"Confirmation" tab**, you could check the **"Restart the destination server automatically if required" checkbox** if you want to install the role immediately. Then click on **"Install"** and you will be bought to the **"Results" tab**. Note that you may close this wizard at any time now, the installation was still continue. Click on **"Close"**.

Once the window is closed, you may view the progress by clicking on the **"flag" icon**(a.k.a **Notification button**) on the top right hand corner of the ***Server Manager***. Once the installation is completed, refresh ***Server Manager*** (by click on the **"refresh" icon** right next the ***notification button***).

Click on the ***notification button***, you will see a **new notification** says that you must **"Post-deployment Configuration"**. Just about every role that you install, will require of some type of **"Post-deployment Configuration"**.


- ### Unintall Roles and Features
Click on **"Manage"** -> **"Remove Roles and Features"**. Then a **"Remove Roles and Features Wizard" window** popped up. On **"Server Selection" tab**, click on **"Next"** to the prompts, choosing the same setting we did when we adding the server role.

When you get to the **"Server Role" tab**, uncheck the **"Fax Server" checkbox**, you will get a **"pop up"** saying that *remove the features that required by the server role*. Notice that this list is not exactly the same as the features we would required to install. This is because you will need to uninstall additional role as well. Click the **"Remove Features" button**. Then uncheck **"Print and Document Services" checkbox**, you will be re-prompted to remove features that required by then role, click on the **"Remove Feature" button**.

Then just **"Next"** until you reach the **"Confirmation" tab**. This time check the **"Restart the destination server automatically if required" checkbox** and then select **"Yes"** to the prompt. Finally, click on the **"Remove" button** and wait for the uninstall to finish and for the server to reboot.

Now you understand how to use ***Server Manager***, and how to install the most important things in the ***Window Server 2016*** which are ***roles and features***.




# Setup Windows Server 2016
1. After the installation, at the very beginning, a blue pane called **"Network"** will be popped from the right, ask you *"Do you want to allow your PC to be discoverable by other PCs and devices on this network?"*, click on **"Yes"**
2. We have to allow the **remote control this server from other computers**. Open the **"Server Manager"**, on the ***main pane* of the "Server Manager" window**, turn on **"remote control"**. And then click on **the value of "remote desktop"**. Then a **"System properties" window** popped up, click on **"allow remote connnection to this computer" radio button**. But make sure to **uncheck** the checkbox just below the radio button called "only allow remote computer of network level verification"
3. We need to enter the ***activation key* for *Windows Server 2016***. Click on **"Windows" icon** -> **"Setting" icon** -> **"System" icon**. A **"System" window** popped up, on the left pane, click on **"About"**. Here is you find the field to input the ***activation key***.



- ## Configure Static IP on the Server
1. We have to **configure a *static IP*** on the server. Open the **"Server Manager"**. On the ***left pane* of the "Server Manager" window**, click on **"Local Server"**. On the ***main pane* of the "Server Manager" window**, click on the **link of the "Ethernet" field - *IPv4 address assigned by DHCP IPv6 enabled***
2. A **"Network Connections" window** popped up, right click **"Ethernet" icon** -> **"Properties"**
3. A **"Ethernet Properties" window** popped up, uncheck the **"Internet Protocol Version 6(TCP/IPv6)" item**, we are not going to be using that. Then select **"Internet Protocol Version 4 (TCP/IPv4)" item**, then click on **"Properties" button**
4. A **"Internet Protocol Version 4 (TCP/IPv4) Properties" window** popped up, click on **"Use the following IP address:" radio button**, fills the following for example:
   ```
   IP address:             192.168.0.10
   Subnet mask:            255.255.255.0
   Default gateway:        192.168.0.1
   ```
   In the **"IP address" field**, you need to make sure that you **set it to the same network** as what your current network is using. **"Default gateway" is the IP address of the network itself**

   Then click on **"Use the following DNS server addresses:"**, fills the following for example:
   ```
   Preferred DNS server:   127.0.0.1
   Alternative DNS server: 8.8.8.8
   ```
   When we set `127.0.0.1` in the **"Preferred DNS Server" field**, this may cause issue because the server right is **NOT** actually a ***domain controller***. In the **"Alternative DNS server" field**, we type in `8.8.8.8` and that simply is a ***Google DNS server***. This will allow you to reach out to the Internet and make an resolve hostnames like ***google.com*** and so forth. Aften that, click on "OK" to close the window
5. We need to **rename the server**. Back to the **"Server Manager" window**, on the left pane, click on **"Local Server"**. On the main pane, click on **the current name of the server** in the **"Computer name:" field**, for example: `WIN-7OOD510FU4`
6. A **"System Properties" window** popped up, click on **"Change" button**. Then a **"Computer Name/Domain Changes" window** popped up, type in the new name in the **"Computer name:" field**, i.e. `SAM`. Then click on **"OK"** close the window. It will require you to restart the server.
7. After the server restarted and logged in, we need to make sure the server is connected to the *Internet* by using ***command prompt*** to ping ***google.com***. You can **pin the *command prompt* to the *taskbar***




# Promote Windows Server 2016 to Domain Controller
Note that any server running **"AD DS" role** is considered a ***domain controller***. We're going to this role to the server and create a **new domain** called **"itflee.com"**. This is the name of an existing website, you can use any name that you would. Note that you won't break the existing website because there is **NO Internet DNS servers** pointing to the domain that were about to create. Once we added the **AD DS role**, we will promote the server as a ***domain controller*** and it will be done.

1. Open the **"Server Manager"**, on the ***right side* of the top menu bar on the "Server Manager" window**, click on **"Manage"** -> **"Add Roles and Features"**
2. On the **"Installation Type" screen**, leave the default option **"Role-based or feature-based installation"** and click **"Next"**. Then click **"Next"** on the **"Server Selection" screen**
3. On the **"Server Roles" list**, check the **"Active Directory Domain Services" checkbox** to add ***AD DS role***. You will see the pop-up window stating that *you cannot install the AD DS unless certain role services or features are also installed*. Click the **"Add Features" button**. Back to the **"Server Roles" tab**, click the **"Next"** to proceed the **"Features" screen**.
4. On the **"Features" screen**, we don't need any additional features, click **"Next"**
5. You will brought to the **AD DS screen**, it tells us it will also need to install the ***DNS server* role** if you have not already set it up. Click **"Next"**
6. On the **"Confirmation" screen**, here we can see the ***roles and features*** we're about to install, click **"Install"** to wait for the installation to finish. Once the installation is complete, you will have ***post-deployment configuration steps*** that you will also need to complete.
7. Click on the **"notification flag" icon** on the top right corner, and click **"Promote the server to a domain controller"**. 
8. The **"Active Directory Domain Services Configuration Wizard"** window popped up, and the wizard will giving us **3 options**:
   - **Add a domain controller to an existing domain** - is for adding additional domain controllers to domain you've already created
   - **Add a new domain to an existing forest** - is for adding a ***child-domain***, also know as ***sub-domain***, if you already have a domain called `itflee.com`, you can create sub-domain called `courses.itflee.com`, which simply to separate our students and teachers from our administrators and developers who reside in the doamin `itflee.com`
   - **Add a new forest** - this will allow us to create and specify a new domain
  
   Choose **"Add a new forest"** option and specify a **"Root domain name"**, in this case, `itflee.com`
9. On the **"Domain Controller Options" tab**, leave **"Forest functional level"** and **"Domain functional level"** as the default which are **Windows Server 2016**. They specify which operating system the ***domain controller*** will use. Then make sure the **"Domain Name System (DNS) server"** and **"Global Catalog (GC)"** checkboxes are checked. If you remember when we installed ***AD DS***, it said that we had to install this ***DNS Server role*** in order for the **DC** to function properly. The **"Global Catalog"** option means that the server will list all ***Active Directory objects***. This is a requirement for the ***primary domain controller***, or when we're creating a **new domain forest**. 
    
    If you choose **"Read only domain controller (RODC)" option**, then a ***domain controller*** will not be able to make changes to the domain. We will want to make changes to our domain, so make sure you do not check this checkbox.

    Type in ***DSRM password*** (***Directory Services Restore Mode***), which allows an administrator to **take an instance of AD offline** for maintenance or troubleshooting. This is not commonly used, but you have to keep the password around just in case. Click **"Next"** to proceed the next tab
10. On the **"DNS Options" tab**, you will see a warning about the ***DNS delegation***, which is about people on the will NOT be able to resolve **local DNS names** on your **local DNS server**, names like `itflee.com`. This is fine because we don't want people on the Internet to be able to access our server. We don't want to be using a domain that's actually a website and causing issues. Click **"Next"** and proceed on the next tab
11. On the **"Additional Options" tab**, the **"NetBIOS" name** is populated for us as **`ITFLEE`**, the **"NetBIOS" name** is an abbreviated version of the ***fully qualified domain name*** (a.k.a **FQDN**) which is `itflee.com`. We're going to leave as the default of **`ITFLEE`** and click **"Continue"**
12. On the **"Paths" screen**, we can see the ***default path*** chosen for the folders that are required by ***AD DS***.
    ```
    Database folder:       C:\Windows\NTDS
    Log files folder:      C:\Windows\NTDS
    SYSVOL folder:         C:\Windows\SYSVOL
    ```
    We recommanded that you leave them at the default settings and click **"Next"**
13. On the **"Review" Options screen**, where we can see all of the options we have chosen so far. If you would like, you can click **"View script" button**, and you'll be presented with a ***PowerShell script*** that you can save in order to later execute and quickly complete the wizard with the same settings we just used:
    ```
    #
    # Windows PowerShell script for AD DS Deployment
    #

    Import-Module ADDSDeployment
    Install-ADDSForest `
    -CreateDnsDelegation:$false `
    -DatabasePath: "C:\Windows\NTDS" `
    -DomainMode "WinThreshold" `
    -DomainName "itflee.com" `
    -DomainNetbiosName "ITFLEE" `
    -ForestMode "WinThreshold" `
    -InstallDns:$true `
    -LogPath: "C:\Windows\NTDS" `
    -NoRebootOnCompletion:$false `
    -SysvolPath "C:\Windows\SYSVOL" `
    -Force:$true
    ```
    Close the ***PowerShell script*** and click **"Next"**
14. On the **"Prerequisites Check" tab**, the wizard is now going to verify that the server is ready to be promoted as a **DC**. Once the checks are completed, at the top you will see that all prerequisites checks have passed.
    
    If you encounter any errors that will not allow you to promote the server as a ***domain controller***, you need to google each error and figure out what's wrong and fix it, usually it's easy to fix. Once you've fixed the errors, click the link that says **"Rerun prerequisites check"**, and wait for the checks to finish again.

    Under the **"View results"** window, we can see that there are various warnings, none of these are critical. You can read it if you like. Click the **"Install" button**, and wait for the installation to complete and the server to reboot, it may takes few minutes.
15. Once the server restart and you'll see the login cover page, you should see the **NetBIOS** name of our domain `ITFLEE` proceeds the user account we are logging into. In this case, `ITFLEE\Administrator`, this is in the format of `[domain name]\[domain user name]`
    
    If you had multiple domains, we could specify a different domain by typing in the `[domain name]\[domain user name]` on the login cover page.

    Once you logged in, the first thing you're notice is a new role - **AD DS** and **DNS** in the **"Server Manager" window**.




# Joining WorkStation to Domain
We're going to join our ***Windows 10*** workstation to our domain.

1. We need to make sure our ***domain controller*** and our ***workstation*** are **connected to the same network**. Run `ipconfig` on ***command prompt***. If your computer has the **IP address `169.xxx.xxx.xxx`**, that means we're **NOT** reaching the ***DHCP server***. It should be grabbing an IP address from your network's **DHCP**. So you change of your ***workstation's IP address*** manually. In this case:
   ```
   IP address:                192.168.0.100
   Subnet mask:               255.255.255.0     // press `tab` to auto complete
   Default gateway:           192.168.0.1

   Preferred DNS server:      192.168.0.10      // DNS Server role IP address
   Alternative DNS server:    
   ```
   Then you can check if the ***IP address settings*** is configured successfully by running `ipconfig` on ***command prompt***.

   Generally, ***"Default gateway"*** is your ***router's IP address*** or the ***IP of your networking switch***. So if you have a ***switch*** that your computer is connected to, you would input that ***IP address*** here.

   The ***"Preferred DNS server"*** is the ***IP address of your DNS server*** that is on your network. In our case, our ***domain controller*** has the ***DNS server* role**, so it's the ***IP address of our domain controller*** which is `192.168.0.10`.

   If we don't configure the ***DNS server*** correctly, we will not be able to join the domain, because the ***DNS server*** is what resolves `itflee.com`, which is the domain that we're going to try and join.
   
   If we have a ***DHCP server* role** installed on a ***doamin controller***, we wouldn't have this issue.
2. We need to rename our workstation and then we're going to join it to the domain. Click on **"Windows" icon (a.k.a Start button)** -> **"Settings" icon** -> **"System"** -> **"About" tab** -> **"Advanced system settings" link**. 
3. A **"System Properties" window** popped up, click **"Change..."**. A **"Computer Name/Domain Changes" window** popped up, type `ITFWS01` in the **"Computer name:" field**, which is stand for ***IT Flee Work Station 01***. And then type `itflee.com` in the **"Domain:" field**. It will require you to restart the computer, click **"Restart"**.
4. Back to the ***Domain Controller server***. Open the **"Server Manager" window**, on the top right meun bar, click on **"Tools" button** -> **"Active Directory Users and Computers"**. **"Active Directory User and Computers" window** popped up, on the ***left pane***, expand `itflee.com`, then click on `Computers` tab, you should see `ITFWS01` workstation on the ***main pane***.




# Windows Domain Controller
***Windows Domains*** have been around since **Windows NT 1993**. They provide ***system administrators*** in an efficient way to manage ***small or large networks***. You only need **only one domain controller** to build ***Windows Domain***, although most one is domains contain several servers and computers.

A ***domain controller*** is any server that has the ***AD DS role*** installed, which stands for ***Active Directory Domain Services***. The server's job is to **handle *authentication request* across the domain**. **A network must have at least one domain controller**.

***Domain controllers*** hold the ***tools*** - ***Active Directory* (a.k.a. *AD*)** and ***Group Policy* (a.k.a. *GP*)** among others, so when you need to **create a new user account or change the main policies**. This is all done from a ***domain controller***.

**You can have several *domain controllers* within a domain, but there is ONLY ONE *primary domain controller* or *main domain controller***. The primary reason for having more than on ***DC*** is ***fault tolerance***. The critical information like ***user and account information* is replicated between the *DCs***. So if one goes down the client computers will switch to the other ***DC*** that is still functioning.

***Domain controllers*** use a tool called ***"Active Directory Users and Computers"***, commonly referred to as ***AD***, or ***Active Directory***. **This tool is used to NOT only manage user and computer accounts, but it also acts as a directory service for *resources on your network*, like *printers*, or *file shares***. When a domain user searches for a new printer to install, they will find all the printers that have been added to the ***domain controller*** with ***Active Directory***. 



## Active Directory & AD Objects
***AD*** is a tool to manage ***domain users***, ***computers***, ***printers***, ***file shares***, ***groups*** and more, these are all considered ***AD objects***. In other words, ***Active Directory*** contains ***objects*** and ***OUs***. 


- ### Groups
***Groups* contain members which can be any valid *AD objects*, a *user*, a *computer*... etc**. By default, there are several ***groups*** that come with ***AD*** like ***domain admins***, ***domain users***, all these ***AD objects*** are stored within folders called ***Organizational Units* (a.k.a. OUs)**.


- ### Group Policy Management
***Group Policy Management*** often called ***GP*** or just ***Group Policy***, which is another important ***tool*** that is located on a ***domain controller***, it allows an administrator to manage all the ***domain users*** or ***domain computers*** remotely. In other words, ***GP*** contains ***GPOs*** and **manage settings for *AD objects***.

***Group Policy*** uses ***GPOs***, stands for ***Group Policy Objects***, to manage the settings of ***valid AD objects***. You can target ***specific AD objects***, specific ***OUs***, or the entire domain if you'd like. Basically, anything you want to create a custom setting for, you can do it with ***group policy***. For example, you can configure the ***desktop backgrounds*** for certain users or computers, what websites they can visit, and ***Internet Explorer*** manage security settings, and countless other settings with ***group policy***.




# Setup Network Address Translation (NAT) to Turn Server into Router



- ## Configuring the Network Interface Cards (NICs)
Before get started, you have to check if the server have at least ***2 Network Interface Cards*** (***NICs***). One ***NIC*** for ***external network***, and another ***NIC*** for ***internal network***.

1. In the **"Server Manager" window**, on ***left pane***, click on ***"Local Server"***. On ***main pane***, click on the **link of the "Ethernet" field**
2. A **"Network Connections" window** popped up, here you should see ***two network adapter icons***. Rename the first network adapter to ***"LAN"***, and then rename the second network adapter to ***"WAN"***
3. You have to setup a ***static IP address*** for ***"LAN"* network adapter** as a default gateway of the local network. For example:
   ```
   IP address:                192.168.1.1
   Subnet mask:               255.255.255.0
   Default gateway:           [empty]

   Preferred DNS server:      127.0.0.1
   Alternative DNS server:    [empty]
   ```
   Note that you need to have a ***DNS server*** setup on the network. It can be the same server where this role is being installed.
4. For the ***"WAN"* network adapter**, you can either **setup a *static IP address*** or **get IP address from *DHCP***. It doesn't matter



- ## Adding the "Remote Access" Server Role
1. Run the ***"Add Roles and Features Wizard"*** through **"Server Manager" window**. Leave everything as default and click **"Next"** until you arrived ***"Select server roles"* tab**.
2. On the ***"Select server roles"* tab**, check the **"Remote Access" checkbox** inside the ***"Roles"* checkbox list**, then click **"Next"**. Then leave ***"Select features"* tab** as default.
3. On the ***"Select role services"* tab**, check the **"Routing" checkbox** inside the **"Role services" checkbox list**, then the **DirectAccess and VPN (RAS) checkbox** is also checked. A smaller window popped up, click **"Add Features"**. Back to the wizard, leave everything as default and then click **"Install"** on the last tab.



- ## Configuring the "NAT router"
1. Open the **"Server Manager" window**, click **"tools"** on the top right menu bar -> **"Routing and Remote Access"**
2. On the **"Routing and Remote Access" window**, on the ***left pane***, you should your server name tab i.e. `TEST123`. Right-click on this tab, then click **"Configure and Enable Routing and Remote Access"**
3. On the **"Routing and Remote Access Setup Wizard" window**, click **"Next"**, it will brought you to **"Configuration"** section and there are **5 options**:
   - **Remote access (dial-up or VPN)**
   - **Network address access (NAT)** - Allow internal clients to connect to the Internet using one public IP address
   - **Virtual private network (VPN) access and NAT**
   - **Secure connection between two private networks**
   - **Custom configuration**
  
   Select **"Network address access (NAT)"**, then click **"Next"**
4. On the **"NAT Internet Connection" window**, select **"Use this public interface to connect to the Internet"** and select **"WAN"**. Then click **"Next"** and leave everything as default.
5. Back to the **"Routing and Remote Access" window**, on the ***left pane***, expand **"IPv4"** -> select **"NAT" tab**. On the ***main pane***, you should see that packets have been translated.




# Adding the DHCP Server Role



- ## Adding DHCP Server using Add Role and Features Wizard
1. Repeat all the steps that described in **"Add Roles and Features"** on **"Server Manager" window**. On the **"Add Roles and Features Wizard" window**, continue through the prompts until you get to the **"Server Roles" tab**
2. On the **"Server Roles" tab**, check the **"DHCP Server" checkbox**. You will be prompted to add the features that are required by the **"DHCP Server" role**, click the **"Add Features" button** to continue. Then click **"Next"** until you get to the **"Confirmation" tab** and click **"Install"**



- ## Configrue DHCP using DHCP Post-Install configuration wizard
1. Once the installation complete, on the **"Add Roles and Features Wizard"**, click **"Complete DHCP configuration" text** on the **"Results" tab**. Or click the **"Notification" icon** at the top of the screen on the **"Server Manager" window**, and select the notification for **DHCP**. The **"DHCP Post-Install configuration wizard" window** will now appear
2. On the **"DHCP Post-Install configuration wizard"**, the first window (**"Description" tab**) tells us that we will need to create the ***DHCP* Administrators and *DHCP Users* security groups**, and authorize the ***DHCP server***, click **"Next"**
3. The next window will be presented with is the **"Authorization" screen**, you need to specify a domain user account that has **domain administrative permission**. By default, it specify the ***account administrator***
   ```
   - User the following user's credentials
     User name:   ITFLEE\Administrator

     User alternate credentials
     UserName:    [empty]

     Skip AD authorization
   ```
   You know that this `ITFLEE\Administrator` account is a domain account because **it prefix by the domain NetBIOS name `ITFLEE\`**, click on **"Commit"**. You will be brought to the **"Summary" page**
4. On the **"Summary" page**, you can see there're two tasks **"Creating security groups"** and **"Authorizing DHCP server"** that are being completed, click **"Close"**
5. Back to the **"Server Manager" window**, on the ***left pane***, now you can the **"DHCP" tab**. You can click on this tab and view information related to **DHCP** such as **"EVENTS"**, **"SERVICES"** and more
6. To open the ***DHCP Management Console***, click on **"Tools"** (at **top right menu bar**) -> **"DHCP"** in **"Server Manager" window**. The ***DHCP Management Console*** will appear and we can see our server is listed along with the **"IPv4"** and the **"IPv6"** setting, but we're only going to dealing with **IPv4**




# DHCP Scopes and Exclusions
A ***DHCP scope*** is a **pool of IP addresses on a specific subnet that can be *leased* by the *DHCP server***. Each subnet can only contain **one scope**, or **continous range of IP addresses**. This means you cannot create a scope ranging from `192.168.0.1` to `25`, and then another scope from `192.168.0.30` to `50`. The scope will instead need to be `192.168.0.1` to `50`, you will need to create ***exclusion*** for the ***IPs*** ending with `25` to `30`.

1. To create a ***DHCP scope***, open the ***DHCP Management Console*** by opening **"Server Manager"**. Click **"Tools"** (on top right menu bar) -> **"DHCP"**
2. On ***left pane***, click on the ***DHCP server*** we want to configure to expand it, in this case, `itfdc01.itflee.com`. Then right-click **"IPv4"** -> **"New Scope..."**. A **"New Scope Wizard" window** will pop-up
3. On the **"New Scope Wizard" window**, continue through the prompt until you get to the **"Scope Name" screen**. This isn't entirely important, it's only for this admin console and no one else is going to see it. For example:
   ```
   Name:             IPv4 Scope
   Description:      192.168.0.2 - 254
   ```
   Click **"Next"** and move onto the next screen.
4. On the **"IP Address Range" screen**, enter your **start and ending IP addresses**. We're starting with `192.168.0.2` because `192.168.0.1` is our ***default gateway***, and we use `192.168.0.254` because `192.168.0.255` is our ***network broadcast address***. The **"Length"** and **"Subnet mask"** are automatically calculated based on the ***IP range*** we specified for the scope, we can leave this setting as default:
   ```
   Configuration settings for DHCP Server
      Enter the range of addresses that the scope distributes.
         Start IP address: 192.168.0.2
         End IP address:   192.168.0.254

   Configuration settings that propagate to DHCP Client
         Length:           24
         Subnet mask:      255.255.255.0
   ```
   Then click **"Next"**
5. On the **"Add Exclusions and Delay" screen**, we're able to specify any ***exclusions*** we may want to create for the scope we entered. Let's say we want to exclude the **IP range `2` to `25`** so we can keep them for our servers
   ```
   Start IP address:       End IP address:
   192.168.0.2             192.168.0.25
   ```
   This range must fall within the scope that we're created. So we couldn't exclude `1` to `25` because we didn't include that `1` in our scope. Once we entered the **IP range**, click **"Add"**, and then click **"Next"**
6. On the **"Lease Duration" screen**, we can specify how long we want the **DHCP lease** to last. The lease is so long the client can keep the **TCP/IP settings** before it needs to come back to the ***DHCP server*** for a **new lease**, or configuration. We're going to keep the default settings of **8 days**, and click **"Next"**
7. On the **"Configure DHCP Options" screen**, leave the default option **"Yes, I want to configure these options now"** and click **"Next"**
8. On the **"Router (Default Gateway)" screen**, we're going to the **local router IP address `192.168.0.1`**, and click **"Add"**. Then click **"Next"**
9. On the **"Domain Name and DNS Servers" screen**, which ask us to specify the ***domain*** and ***IP address*** of our ***DNS server***. This information is automatically propulated with the ***IP address*** of our **DC and DNS server**, which is `192.168.0.10`. Click **"Next"**
10. On the **"WINS Servers"**, which allow us to specify a **WINS Servers**. A **WINS Servers** works much like a ***DNS server*** and that it relay host names with IP addresses but it uses different protocol in ***DNS***. We do not have a **WINS Server** because ***DNS* has replaced this out-of-date features**. Click **"Next"**
11. On the **"Activate Scope" window**, click **"No, I will activate this scope later"**, then click **"Next"**, and **"Finish"** to complete the wizard
12. Back to the ***DHCP Management Console***, we can now see the new scope that we just created on the ***left pane*** - **"Scope[192.168.0.0] IPv4 Scope"**. Notice the ***red down arrow*** inside of the icon, this means that the scope has **NOT** been activated. We can go ahead and right-click on the scope (***tab***), and select **"Activate"**
13. Expand **the scope on the *left pane*** - **"Scope[192.168.0.0] IPv4 Scope"**. Here you can see the **"Address Pool"**, **"Address Leases"**, **"Reservations"**, **"Scope Options"** and **"Policies"**.
    
    - The **"Address Pool"** is the **list of available IP addresses**, as well as all exclusions.
    - The **"Address Leases"** shows all the client computers who have received **TCP/IP configuration** from **DHCP**
    - The **"Reservations"** simply list all the computers that have a ***DHCP reservations***
    - The **"Scope Options"** allows you to change other network settings like ***default gateway***, refer to here as a ***Router***, ***"DNS Server"*** and ***"DNS Domain Name"***
    - The **"Policies"** allows an administrator to assign certain **IP address ranges** to certain devices like ***IP phones***, ***desktop computers***, ***printers*** and ***unknown devices***




# Introduction to DHCP



- ## Static IP Address
Before you can understand the ***DHCP***, you need to understand ***static IP address***. A ***static IP address*** is manually assigned by administrator, and it is not change unless you manually change.

In order to configure the **static IP adderess**, you must know the basic **TCP/IP settings** for your network. Things like **available IP addresses**, what **subnet mask** to use, what **gateway** to use, and optionally what **DNS servers** to point your computer to.

If you enter an invalid settings, your computer will not have network connectivity until you fix the configuration issue.



- ## DHCP
***DHCP*** stands for ***Dynamic Host Configuration Protocol*** is a networking protocol that allows a particular server to assgin **TCP/IP** configurations automatically to client computers on the same network.

In the ***Windows*** world, you need to install ***DHCP server role*** on the ***Windows Server*** in order for that to have this functionality on your network. A ***DHCP server*** will automatically configure the ***IP address***, ***subnet mask***, ***DNS server address***, and ***gateway of client computer*** which is any computer on the network that is attempting to use ***DHCP*** as its ***network configuration***.

In other words, DHCP is a network protocol, and in the ***Windows*** world, is installed as a ***server role***. System administrators can specify a single scope, or range of IP addresses for DHCP to assign to clients, and this is on per subnet, so **only one scope per subnet**.

**If a computer is configured to use DHCP, but it cannot find a DHCP server. It will assign itself a private IP address that start with `169.254.x.x`.**


- ### DHCP Lease
The **configuration of *DHCP* assign is NOT permanently giving to the client computer, but instead it leased to the client for a certain amount of time.** Once the ***DHCP leases*** are expired, the client computers must reach back to the ***DHCP server*** and renew its ***existing lease***, or it must obtain the entire ***new configuration*** and ***lease***. In other words, the configurations handed out by DHCP are leased and must be renewed regularly.


- ### Before DHCP
Before ***DHCP*** was used, ***system administrator*** need to go to each computer and manually configure the **TCP/IP settings** before it was on the network. This was bad for several reasons:
1. It takes a long time, what if you have thousands of new computers
2. There's large room for user error, what if an administrator assigned the same IP address to two different computers



- ## Metaphor for DHCP Working Mechanism
*Johnnie* is taking a trip and has arrived at his hotel. He walks inside the hotel and asked the clerk for a room. The desk clerk then looks in his registry to see which rooms are available and finds all the rooms on the top floor are closed because they're being repainted. It's an example of ***DHCP exclusion***. Its room or IP addresses cannot handed out to clients:

|Hotel | | | | |
| - | - | - | - | - |
| 301 X | 302 X | 303 X | 304 X | 305 X | 
| 201(O) | 202 | 203 | 204 | 205 | 
| 101(R) | 102(R) | 103(R) | 104(O) | 105(O) | 

The clerk finds that the first 3 bottom rooms have been reserved, so he can't give those rooms to *Johnnie* either. This would be an example of a ***DHCP reservation***. The people aren't in the rooms yet, or the IP addresses are not taken necessarily, but they cannot be handed out because they're reserved for other people or other computers.

Just because an IP address or room is reserved, it does not mean that's not in used or is in used, all it means it that no one can go into this room, or use this IP address because it reserved for another client.

The clerk also notices that room `104`, `105` and `201` are occupied, so he can't give him any of those rooms either. This would an example of computers just taking IP addresses from ***DHCP*** they're as available.

He sees that he can give *Johnnie* room `202` for one week. Now the one week would be equivalent to the ***DHCP lease***, you can specify when you configure ***DHCP*** how long client computers can stay in a room, or they can keep an IP address. By default, ***DHCP lease*** is **eight days**, but that doesn't apply to those who reserved IP addresses. ***Reservation*** and ***DHCP*** are indefinite.

Finally, our clerk sees that he give *Johnnie* room `202` for one week, or the lease duration, whatever we configure in ***DHCP***. *Johnnie* accepts the room and goes inside. The clerk now updates his registry to note that there is now a person in room `202`. So the next person that shows up at the desk is not going to get room `202`. ***DHCP*** does the same thing when it hands out a client IP address to a client. It remembers that it gave this IP address to this computer and will not hand it out again to another computer.

At the end of the week, if *Johnnie* decides he wants to stay in the hotel, he's going to have to go back to the clerk and ask for another week. Now the clerk can either give him another week in his existing room, or he can assign him a new room for another week. ***DHCP*** works very similar to this, when the client computer's ***DHCP lease*** expires, it comes back to the server and he either gets an extension with his existing IP address, or ***DHCP*** hands at a whole new IP address and a whole new lease.

***DHCP*** works very similar how our hotel works, administrators may specify the range or scope of IP addresses that are to be supplied by ***DHCP***, as well as excluding or prohibiting certain IP addresses from being assigned to clients. Just like our hotel clerk did for repainting the rooms on the top floor.

You may also set reservations for specific computers, you could reserve the IP address `192.168.1.10` for the MAC address of the server `ITFDC01`. Only this server would be able to get that IP address from ***DHCP***. This is different from manually configure the IP address because we are going to configure the IP address from the ***DHCP server***, and not the client computer.

If you have a computer that is configured to use ***DHCP*** **but it has an IP address starting with `169.254...`, this is referred to as a *private IP address*. It means that the computer was unable to find a *DHCP server* on the networkf, so it assigned itself that IP address**.

To conclude, you can exclude a range of IP addresses, make IP reservations for individual MAC addresses.


- ## Technical Explanation of How DHCP Works

| Windows Server | -connected- | Switch | -X-disconnect-X- | Windows Workstation |
| - | - | - | - | - |
| **Configuration** | | | | **Configuration** |
| IP: 192.168.1.10 | | | | **DHCP Enabled** |
| **Server Roles** | | | | IP: 169.254.x.x |
| **DHCP** 192.168.1.100 - 200 | | | | |

In this example, we are only showing two computers in a switch. Right now, the Windows workstartion is not plug into the switch. Since it cannot find the DHCP server, it has assigned itself a private IP address.

Once you plug in the network cable into the switch, the client computer become broadcasting a ***DHCP discover request***. The request is sent to the entire network and hopes the message will reach the DHCP server.

**A DHCP server will be listening for this request**. Once it received the DHCP discover request, it will send back a ***DHCP offer***. This includes all the DHCP IP settings like IP address, subnet mask, DNS server and gateway.

Once the client receives the DHCP offer, it will send back a ***DHCP request*** to the server, this message lets the DHCP server know that the client wants to keep the settings that were offer by the DHCP server.

Finally, the DHCP server will send back an **acknowledgement message** stating they understands the client computer is going to keep the setting and it offer. The computer will accept the ***DHCP IP configuration***, and its work with DHCP is done.


- ### DORA
We can memorize this process for ***Discover***, ***Offer***, ***Request*** and ***Acknowledgement*** with the acronym ***"DORA"***, which is the technical process of getting client IP addresses.

The client sends out a **DHCP discover message** and a **DHCP server response** with the **DHCP offer**. The client request the offered settings and the server acknowledges the request.


- ### Reasons Using Static IP Address
Remember that one of the settings that the DHCP can automatically configure is the DNS server, its configuration with specified the static IP address `192.168.0.10`. What if the DNS server use a DHCP, and its IP address changes from week to week, or everytime its lease expired. We would need to update our DHCP settings with the new IP address everytime it changed.

We can't think of a single circumstance where you would want to do this. It's much less complicate to simply assign a static IP address to a DNS server so it never changes.

Another other examples would be printers and scanners, you want these devices to use a static IP address so people would be able to consistently print to them, and not need to re-enter the IP address everytime its lease expired.

Static IP addresses are still relevant for things like servers and printers, and if your DHCP server crashes, computers relying on DHCP will stay connected until their TCP/IP lease expires.


- ### Manually Setting Static IP Address on Client vs Configuring DHCP Reservations on DHCP Server
You may be wondering why we would take the time to log on to each client computer and manually configure a static IP address, or we can simply create a DHCP reservation from a single server.

There is one major different, if your DHCP server crashes and you manually log out the computer and set a static IP, that computer will not lose network connectivity. On the other hand if you create a DHCP reservation, that client computer is depended on the DHCP server. If the DHCP server goes offline for any reasons, whether it is a crash, and its network connectivity issue, maybe a switch goes down, or a cable gets cut, then that computer will lose its DHCP configure IP address as soon as its lease expired.

So basically the server is only up for as long as the DHCP server is up. Obviously, the point of DHCP is to make life easier when connected to the new devices to a network and getting them online quickly. **So servers, printers and other things that offer services to a network uses a static IP address, a manually configured IP addresses that it's NOT relying on DHCP. And workstations, or end users, people who are connecting to their laptops, their desktop computers to utility this server are using DHCP as a network configuration**.




# DNS Resource Record Types
DNS servers hold different types of entries, which are called ***Resource Records***. These resource records are used to provide DNS based data about computers on the network.

We're going to provide a general overview of the **most common types of resource records** that you will encounter while working on DNS:
- **SOA** - stands for ***Start of Authority resource record***. Every zone contains an **SOA resource records** at the beginning of the zone. The SOA resource record contains information about the DNS server that has provided the data for that particular zone.
- **NS** - stands for ***Name Server resource record***. The NS record indicate the zone authoritative DNS service. Every zone must contain at least one NS record at the root of the zone.
- **A** - ***A resource record*** maps an **FQDN** (Fully Qualified Domain Name) to an IP address. An example of FQDN would be `itfdc01.itflee.com`:
  ```
  itfdc01.itflee.com -> 10.0.2.10
  ```
- **PTR** - stands for ***Pointer resource record***, which does the exact opposite of an A record by mapping an IP address to a FQDN:
  ```
  10.0.2.10 -> itfdc01.itflee.com
  ```
- **CNAME** - stands for ***Canonical Name resource record***, which creates an ***alias*** for a specified FQDN. For example, if you have the FQDN of `itfdc01.itflee.com`, but the server's name was changed to `itfleedc01.itflee.com`. You could create a CNAME resource record to point all traffic headed to `itfdc01.itflee.com` to `itfleedc01.itflee.com`:
  ```
  itfdc01.itflee.com > itfleedc01.itflee.com
  ```
- **MX** - stands for ***Mail eXchange resource record***, which is used to specify email service for the zone. If you do not have a mail servers such as ***Exchange Server 2010***, then you will not use or see this type of entry.
- **SRV** - stands for ***Service resource record***, which allows you to specify servers for particular services or protocol. For example, if you're writing a web serve a new domain, you could create a SRV resource record and specify the FQDN and the port of the server so it will be easily accessible to anyone who queried your DNS server.

