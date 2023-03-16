# Windows Server 2016 - part 2




# Active Directory Users and Computers
***Active Directory Users and Computers*** also known as Active Directory, or AD, which is a tool that installed when a server has a ***Active Directory Domain Service* role** installed.

Active Directory is a ***live directory* or *database*** that stores user accounts and their passwords, computers, printers, file shares, security groups, and their respective permissions. Each of these are considered they're own objects, but a group contains nothing but other objects. A group could be made up of other active directory users, or computers, printers, or file shares.

The reason for using **group** within Active Directory is frequently for security purposes. **You can use AD and Group Policy together to assign specific permissions for objects within Active Directory**. You can either for groups or just particular computers or particular users. 

**The purpose of Active Directory is to handle security authentication across the domain.** One of the ways AD does this is by only allowing authorized users to log on to the network. Active Directory also provide central security management of your network resources by storing things like user names, passwords in one location instead of the administrator need to store these informations on each individual computer.

The most common tasks to do with the Active Directory is **reset user passwords**, and **create or delete user accounts**. For example, everytime a new employee is hired in your company, they would need login credentials. You would need to create their user accounts and help them log in for the first time. Often, people would forget their passwords, and you will be asked to reset for them. And you'll use Active Directory to do this.

If you do not have Active Directory, you would need to create a local account on each computer that the new employee would need to access. So if you have 5 computers, and the employee need to access all 5, you need to create 5 user accounts. Also, everytime you need to reset a password for that user, you would need to do it on each computer they had accounts on. This is not a big deal for handful computers, but what happens when you have 200 computers on network, or 1000, or 100,000. You obviously can't go and reset password on each computer for each user account. Because you're going to get multiple password requests a day. You might have 10 or 15 people every day that forget their passwords and you need to reset it for them.

So Active Directory solve this problem by having all the accounts stored in one place. When a user tries to log into a **domain joined workstation**, the computer reaches out to the domain controller, and checks the entered credentials against the credentials that is stored in Active Directory. This means that when a user changes his password in Active Directory, the change would be effective for all domain computers on the network. So if you have 1000 computers, they change it in one spot on the domain controller, and that is effective for all the computers or whatever the number of computers that they needed to access. This examples are not only applies to user accounts, but the other objects that can be stored in the Active Directory like computers, printers, file shares and groups.



- ## Using Active Directory on Windows Server 2016
Open the **"Server Manager"**, on the top right menu bar, click **"Tools"** -> **"Active Directory Users and Computers"**. An **"Active Directory Users and Computers" management console window** popped up, the ***left pane*** is the ***navigation pane***, and we have the ***content of current location*** on the ***main pane***.

On the top menu bar, we have **"File"**, **"Action"**, **"View"** and **"Help"**. Within the **"File"** menu, you can either **"Exit"** Active Directory or select **"Options..."**. 


- ### "File" -> "Options"
Within **"Options" window**, you can delete any changes you've made to the view of Active Directory Users and Computers, that is the console.


- ### "Action"
The **"Action"** menu is the **same exact Action menu** you would get if you right-click on an object:
- -
  - Delegate Control...
  - Find...
  - Change Domain...
  - Change Domain Controller...
  - Raise domain functional level...
  - Operations Masters...
  - New           >
  - All Tasks     >
  - Refresh
  - Export List...
  - Properties
  - Help

If you select `itflee.com` on left pane, and you click **"Action"**, you will notice that **these options are the same exact set of options you'll get if you simply right-click `itflee.com` on the *left pane***.


- ### "View"
The **"View"** menu allows you to add or remove columns as necessary to show or hide information. It can be makes thing a lot quicker if you try to find a certain field and you looking for a bunch of objects inside the Active Directory. Most importantly, inside of this **"View"** is the **"Advanced Features"**, this viewing mode shows a lot of hidden and useful information that you would otherwise not be able to find.

- The **"View"** -> **"Filter Options..."** allows you to show or hide certain types of object types within the contents:
  - Users
  - Groups
  - Contacts
  - Computers
  - Printers
  - Shared Folders
  - Services

This could be useful if you only want to find **"Users"**, or if you only want to  **"Groups"**, and you have a bunch of different object types stored within the same **Organizational Unit**.

- The **"View"** -> **"Customize..."** option allows you to futher customize your view within Active Directory Users and Computers console by showing and hidding different component:
  - MMC
    - Console Tree                              // left pane
    - Standard menus (Action and View)
    - Standard toolbar
    - Status bar
    - Description bar
    - Taskpad navigation bar
    - Action pane
  - Snap-in
    - Menu
    - Toolbars

For most administrators, the default options are work just fine.


- ### "Help"
The **"Help"** menu allows you to quickly access **"Help Topics"**, and the **"TechCenter Web Site"**. You can also view the **version** of the ***Microsoft Management Console*** (**MMC**) and Active Directory Users and Computers by clicking the **"About Microsoft Management Console..."** and **"About Active Directory Users and Computers..."**.



- ## Action Buttons Below the Menu
Below the menu, you can see several action buttons. First, you have **navigational buttons** like going forward or backward. You can hover over each of the buttons and learn what they do by reading the tooltip that would automatically appear.

The menu of the action buttons would change depending on if we have a **domain controller** selected (i.e. `itflee.com`) or **OUs**. And sometimes it would change for the particular objects it selected inside of the OUs, or the container.



- ## Tool Bar
On the **right side** of the action buttons menu, we've a tool bar. We can create a user, we can create a new group, or we can create a new Organizational Unit in the current container. We can also set **filter options**, that's the same as going to **"View"** -> **"Filter Options..."**.

Next, we have the **find object in Active Directory**, and this is important. If we click this button, we can search for different objects like **"Users, Contacts, and Groups", "Computers", "Printers", "Shared Folders", "Organizational Units", "Custom Search" and "Common Queries"**. 

If you need to find something on the Active Directory, the most important thing you need to remember by default, whatever OUs you're residing in. So if you want to search the entire domain, you can select **"itflee.com"**. Or you might have **multiple domains**, you can click **"Entire Directory"**. **"Entire Directory"** will always cover the most area as possible. If you just want to just do the broadest search, you can search **"Entire Directory"** and type in your search, then just click **"Find Now"**. You can just click **"Find Now"** and leave the search field empty to discover every object that is in your domain or in **trusted domain**.

On the left pane, select **itflee.com** -> **Users**. You can select particular user here and you can click this **"Adds the selected objects to a group you specify."** button to add user to selected group. And it has selected object to the a group you specify. By clicking on that user and clicking this button, we can type in a group like **"domain admins"**, or anything we would like, and then just click **"OK"**. We can quickly add them to that group.



- ## Navigation Pane of Active Directory Users and Computers Console
On the left side of the console, we have the ***navigation pane***. At the top, you will see the **"Saved Queries" tab**, and the name of your domain `itflee.com` in our case. **"Saved Queries"** is a commonly ignored by many administrators. It allows you to quickly locate things like expired or locked out user accounts, user accounts are not login in the last 30 days and more. As the name implied, you can quickly searches and save them for later use. This could make redundant tasks so much easier, like a lot of times you'll have hiring manager or someone who's trying to secure the domain will say *I want to know who hasn't logged in the last 30 days and I want you to disable or delete their accounts*, and you can do that with **"Saved Queries"**.

- `itflee.com` refers to the domain that Active Directory is servicing, you may right-click on the domain (on the ***Navigation Pane***) and the complete several actions.
  - Delegate Control...
  - Find...
  - Change Domain...
  - Change Domain Controller...
  - Raise domain functional level...
  - Operations Masters...
  - New           >
  - All Tasks     >
  - Refresh
  - Export List...
  - Properties
  - Help

- #### Delegate Control Option
First, you can delegate the control of the domain, and this will allow you to choose additional users who may manage the domain.

- #### Find Option
The **"Find..."** button allows you to locate object store within this domain, it's the same as clicking this little search button uphere (on the **tool bar**).

- #### Change Domain Option
You may change domain by selecting the **"Change Domain..."** option, you would use this option if you have a subdomain or another trusted domain on your network.

- #### Change Domain Controller Option
You can also change to another domain controller by using the **"Change Domain Controller..."** button. Since we only have one domain controller in our network, we aren't going to be able to do this.

- #### Raise Domain Functional Level Option
The **"Raise domain functional level..."** option is used to enable Active Directory features **when you have multiple domain controllers on a network that are not the same version**. Some features are only available when all your servers are updated to the latest version available. For example, if you have a ***Windows Server 2012*** domain controller and a ***Window Server 2016*** domain controller both servicing the same network, your **domain functional level** would be that of the ***Windows Server 2012*** domain controller, means the server cannot use some of the new features from the ***Window Server 2016***, but they could only use the features included with ***Windows Server 2012***. Now if you were update the server from ***Windows Server 2012*** to ***Window Server 2016***, we can then come back to the screen, and raise the domain functional level to that of ***Windows Server 2016*** to enable the new features.

- #### Operations Masters Option
The **"Operations Masters..."** option allows you to choose which server operating master role like the ***schema master***, ***domain name naming master***, ***relative identified master***, ***primary domain controller emulator*** and the ***infrastructure master***. If you have multiple domain controllers on your network, you can change which server have what roles. This is something you would need to do when you remove a domain controller from the network. If you had a domain controller on the network that had the primary domain controller emulator, or PDC emulator, and you wanted to remove that domain controller from the network, you'd first want to remove the role from that domain controller and transfer it to another server. In the **"Operations Master" window**, you would click **"PDC" tab** and then click **"Change..."** after the typed in the new PDC FQDN. If `ITFDC02.itflee.com` was holding the PDC server role, and we want to remove it off the domain. We could do that right here by clicking the **"Change..."** button and switching it over to `ITFDC01.itflee.com`. And then we would be free and clear to remove that server from the network.

Active Directory Domain Services is a ***multi-master enabled database***, which means that **several domain controllers can make changes to this database**, allowing multiple DCs to write changes to the database can sometimes cause conflicting updates to occur. This was where operation masters steps in to resolve issue by only allowing certain DCs to make changes to certain parts of Active Directory Domain Services. So that's why you don't want to have several domain controllers trying to act as the ***RID*** or Relative Identifier master, because it's just to have one dowmain controller who's responsible for that, and that way you don't have conflicting updates happening from two different servers.

Since we did not have any additional domain controllers on the network, we cannot change any of the operation master settings.

- #### New Option
The **"New..."** option allows us to create new objects within Active Directory like user accounts, computer accounts and more:
- -
  - Computer
  - Contact
  - Group
  - InetOrgPerson
  - msDS-ShadowPrincipalContainer
  - msImaging-PSPs
  - MSMQ Queue Alias
  - Organizational Unit
  - Printer
  - User
  - Shared Folder

- #### All Tasks Option
The **"All Tasks"** option is basically the same options that we have up here (all options above **"New"**).

- #### View Option
The **"View"** option which is exactly the same as **"View"** in top menu bar.

- #### Export List Option
The **"Export List..."** option is allows us to export a list of the content's domain to a text file.

- #### Properties Option
We can find about information about the name and the description, and who manages the domain.


- ### Right-Clicking Organization Unit
You can do the same for right-clicking on any objects within there. For example, for an **Organizational Unit**, you can export a list, you can view properties, you can filter options, create a new **Organizational Unit**, Computer, Contact, whatever you would like to do.




# Organizational Units (OUs) and Containers
***Container*** is a structural object that included by default within Active Directory. The most important different between **OUs** and container is that you cannot apply ***Group Policy Objects*** **GPOs** directly to containers.
 
It's also not possible to create a container in Active Directory although you can use ADSI edit to create container if you have that requirement, most of the time, you will never need to do this, but there will be some scenarios where you're launching a new program or a new management software suite like ***System Center Configuration Manager*** **SCCM**, and it will require you to create containers, and you'll use **ADSI** to do this now, by default the containers you will immediately see in Active Directory are **"computers"**, **"ForeignSecurityPrinciples"**, **"Managed Service Accounts"** and **"Users"**.



- ### Computers Container
The **"Computers"** container is the default location for new computers who join a domain, so when we join a new workstation to this domain if we pop in here (***main pane*** while **"Computers" tab** selected), it would be listed under this container by default. You can change that with ***PowerShell*** but by default, this is where it's going to land.

Note that ***Group Policy Objects*** are applied to the `itflee.com` domain like the default domain policy, will apply to this **"Computers"** container, **but you CANNOT hang specific GPOs to this container**. So it's therefore not a good practice to leave computers inside of the computers container. It's better to build out an **OU**, then give it a name, and apply **GPOs** inside of that **OU** and place your computers inside of that **OU**.


- ### ForeignSecurityPrincipals Container
The **"ForeignSecurityPrincipals"** container holds **proxy objects** for security principles from other trusted domains. A security principle from another domain could be a user account or a security group that resides in the other domain. If you do not establish a trust between your domain and another, you will not be using this container. An example of when you'd want to use one of these **proxy objects** would be allowing a user from another domain to also be a part of the administrators group in your domain. In this case, you would add the **proxy objects** that represents the user from the other domain to your administrative group, and it would stored inside of this **"ForeignSecurityPrincipals"**.


- ### Managed Service Accounts Container
The **"Managed Service Accounts"** container holds accounts that are used to run service or applications that are run on servers. Now since managed service accounts (a.k.a. **MSAs**) are supposed to be used for services and not by end-users, you will not create passwords for these accounts, but they are instead handled automatically. The problem of expiring service account passwords and security can be a huge headache for administrators. And this is what **MSA** is hope to solve. If you notice this administration that make any sense to you, basically there's user accounts that are created within Active Directory that are only used to complete services like it might be a ***virus scanner***, or installing updates, or a program that needs to reach out and do a certain script.

A lot of time, we would create these regular user accounts that would be the same as any other user account cross the domain, but you would have to make sure you maintain the password, and your applications would have to know what the passwords were, so if you change the password in Active Directory, then you have to go back to your application and update the password there. **MSAs** are designed to make it much less complicated, where you just create the account and you don't ever have to deal with passwords, or expiring accounts, or anything silly like that.

To create **MSA**, you need to the ***PowerShell*** command line, there is no interface to do this at this time although Microsoft made later add this functionality.


- ### Users Container
Inside of the **"Users"** container, if we pop this open (click **"Users" tab** on ***navigation pane***), you're going to find the administrator and guest user accounts, as well as several default security groups which are used by your domain. So here (***main pane***), you can see the **"Guest"** which is disabled. The **"DefaultAccount"** which is disabled. And then we have the **"Administrator"** account, and then we have all these security groups (i.e. ***Domain Admins***, ***DnsAdmins***) that are used by your domain.


- ### Builtin Domain
The **"Builtin"** domain contains security groups that are required for your domain operate. So if we pop in here (click **"Builtin" tab** on ***navigation pane***) we can see there's the **"Administrator"** group, **"Guests"** group, **"Hyper-V Administrators"** group, **"Replicator"** group, a big one is a **"Remote Desktop Users"** group. The thing you keep in mind is that **you CANNOT delete these group**.



## Organizational Units
By default, we have the **"Domain Controller" organizational unit**, this is where our computer `ITFDC01` will be stored. By default, there is a ***Group Policy Object*** that is created and applied to this **OU**.

***Organizational Units*** commonly refer to as **OUs**, are used to organize and separate objects within Active Directory. The objects could be anything that Active Directory could store, so it could be a user account, computer, printer, or a file shares.

If your company have a marketing team, you might create a new organizational unit and call it **"marketing"**, and store all your marketing users and computers inside of this **OU**. So just like it sounds, the purpose of **OUs** are help you organize your domain within Active Directory. But much more important than just having a tidy Active Directory or an organized Active Directory.

A lot of time, system administrators will assign specific permissions to certain **OUs**. For example, all the users instead of the **marketing OU**, may have a special desktop background and special permission to a file share that others may not have. This is why it's very important that you insert Active Directory objects into the correct **OU** as picking the wrong **OU** could lead to some users having security privileges that are not supposed to have. This not only applies to user accounts but every object that is stored within Active Directory.


- ### Create Organizational Unit
To create an organizational unit, we need to right-click in the desired location. In this case, we're going to right-click `itflee.com` on the left pane of the Active Directory Users and Computers MMC. Then select **"New"** -> **"Organizational Unit"**. Then we have a new little wizard called **"New Object - Organizational Unit"**, in the **"Name:"** field, type in the name of the **OU** that you want, we're going to type ***"Test OU"*** for demonstration purposes. Below the **"Name:"** field, we have a checkbox called **"Protect container from accidental deletion"**. **You always have to leave this check**, unless you plan on deleting it very soon. We're going to leave this check. Then you should check **"OK"**.

Back to the Active Directory Users and Computers MMC, look at the left pane, by default we've navigated the **"Test OU"** and you can it listed over here:
```
Active Directory Users and Computers
  > Saved Queries
    itflee.com
        Bulitin
        Computers
        Domain Controllers
      > ForeignSecurityPrinciple
      > Managed Service Account
        Users
        Test OU                   // highlighted
```
If we go back to the domain `itflee.com` (click on it), we can see we have a new Organizational Unit called **"Test OU"**. If we right-click the **"Test OU"** on left pane, you can see we can **"Cut"** the **OU** if you want to move it, we can **"Delete"**, **"Rename"** and **"Refresh"** the **OU**.

We can also make another **OU** inside of this **OU**. So if we right-click on the **OU** and choose **"New"** -> **"Organizational Unit"**. The same wizard appeared and we can called this **"AnotherOU"** and just click **"OK"**. So we have an **OU** within an **OU**, we can keep going down and down, as deep as we need to go to keep our domain organize:
```
Active Directory Users and Computers
        ...
        Test OU
          AnotherOU
```
Keep the in mind, you have to **left-click on the OU at first**, and then **right-click on that OU `Test OU`**, you will this action menu right here (including **"Export List..."**). But if you **left-click on the domain `itflee.com` at first**, and then **right-click on that OU `Test OU`**, **you will NOT get the same options, so you cannot export a list for **example**.


- ### Export List Option
Now we left-click **"Test OU"**, and then right-click **"Test OU"** again, now we can choose **"Export List..."**. **This will create a list of a text document `.txt` that will list all the objects within this OU, it is NOT recursive, so it wouldn't list any objects inside of the "AnotherOU"**.

If we click on the **"Export List..." option** on the **"Test OU"**, and we save it as **"TestOU.txt"**. And then we go to the desktop and click on **"TestOU.txt"**, you will see that we have **"AnotherOU"**:
```
Name    Type    Description
AnotherOU       Organizational Unit
```
If there were another objects residing inside of this **OU**, it would be listed. Just like the root domain, we can right-click it and we can **"Delegate control..."**, but 9 times out of 10 all you going to do with **OUs** is creating or deleting new **OU**.


- ### Protection from Accidental Deletion and How to Delete OUs
To delete an **OU**, we simply right-click (**"Test OU"**) and choose **"Delete"**. A dialog box popped up and say ***"Are you sure you want to delete it..."***. If we're going to say **"Yes"**, another dialog box popped up and say ***"You do not have sufficient privileges to delete Test OU, or this object is protected from accidental deletion"***. If you remember when you created this **OU**, we checked the checkbox that said **"Protect container from accidental deletion"**. The way to turn this protection off is go back to the Active Directory Users and Computers MMC, up here to the top, we select **"View"** -> **"Advanced Features"** on the **standard menu**. Then on the left pane, we have a ton of option overthere, it will be a little confusing:
```
itflee.com
  > Builtin
  > Computers
  > Domain Controllers
  > ForeignSecurityPrinciple
  > Keys
  > LostAndFound
  > Managed Service Accounts
  > Program Data
  > System
  > Test OU
  > Users
  > NTDS Quotes
  > TPM Devices
```
We can see that **"Test OU"** is still here. If we expand this out, we can see **"AnotherOU"**:
```
  ...
    Test OU
      > AnotherOU
  ...
```
When we right-click **"Test OU"** and choose **"Properties"**. Then a **"Test OU Properties" window** popped up, and we'll get to the **"Object" tab** at the top, here we can uncheck **"Project object from accidental deletion"** checkbox, and we click **"OK"**. And we'll do the same thing on **"AnotherOU"**. Then we go back to the Active Directory Users and Computers MMC, click on **"View"** -> **"Advanced Features"** to turn off the **"Advanced Features"**. Now we can delete these **OUs** by right-clicking **"Test OU"** -> clicking **"Delete"** on the left pane of the MMC. We're going to get a popped up says **"Object Test OU contains other objects. Are you sure you want to delete object Test OU and all of the objects it contains"**, we're going to click **"Yes"**. Now you can see that we have successfully deleted.




# Creating and Managing User Accounts
We're going to create and manage user accounts within **Active Directory Users and Computers MMC**. This is the most common task you want to fully understand if you want to have a successful career as a **Windows Server adminstrator**.

When it comes to creating and managing user accounts, you really have 2 options. The first is to use the **Active Directory Users and Computers MMC**. Secondly, you can use the **PowerShell command line**. 9 out of 10 administrators prefer the **Active Directory Users and Computers MMC**, because it's just easier.

Now open the **Active Directory Users and Computer MMC** by clicking **"Tools"** (on the *top right menu bar*) -> **"Active Directory Users and Computers"** on the **"Server Manager" window**.

In the MMC, if you expand the domain `itflee.com`, you can see that we don't really have any kind of structure setup, just the default organizational untis and containers. So if you're at your workplace, if you already have a structure setup, you should go with what you have. In our case, we're going to create our own structure.

We're going to pretend we work for a company called **"itFlee"**, so the first we're making an organizational unit called **"itFlee"**. So we're going to right-click on the root domain `itflee.com` on the left pane, then click **"New"** -> **"Organizational Unit"**. Then we're going to called this **"itFlee"**.

Inside of this **"itFlee" OU**, we want to have an **"Administrators" OU**, where we can put all our domain administrators, and then we want to have an **"users" OU**, where we can put all of our users, people who just work on the computers, or just need to login, but don't necessary need to make administrative changes on the computers.

So we right-click on the **"itFlee" OU** on the left pane, and then click **"New"** -> **"Organizational Unit"**. We're going to call it **"Administrators"** and then click **"OK"** on the **"New Object - Organizational Unit" pop-up**. And then we will do the same thing again, right-click on **"itFlee" OU**, and then click **"New"** -> **"Organizational Unit"**, and we'll make one for just users. So let's call this **"Domain Users"**, and click **"OK"** on the pop-up.

Now we have some kind of structure within our domain (on the ***navigation pane***):
```
Active Directory Users and Computers
  > Saved Queries
    itflee.com
      > Bultin
      > Computers
      > Domain Controllers
      > ForeignSecurityPrinciples
      > Managed Service Accounts
      > Users
        itFlee
          Administrators
          Domain Users
```
The type of design is entirely up to you, and how you want to organize your Active Directory objects is entirely is your decision. You may design to put both Administrators and Users in the same **OU**, or you might design to put them in separate **OUs** like we did.

So far, we've been using the **administrator account**, that were setup by default on the server. This practice is generally found on the security role as share user accounts are considered a bad practice, because if let's say you have 5 administrators and they're all using the same account. If one person deletes a file, or steals a file, and you look at the logs, and everyone using the same account. It's going to be hard to tell who is actaully completed the changes or whatever the case was. It's better to create a new user account and only use the **default administrator account** as a backup.

We're going to create a new user account for ourselves under the **"Administrators" OU**. We want ourselves to be an admin. We're going to right-click on the **"Administrators" OU**, then click **"New"** -> **"User"**. A **"New Object - User" window** popped up, we fill all the information as follow:
```
First name: Paul    Initials: [empty]
Last name:  Hill
Full name:  Paul Hill

User logon name:
paul.hill[@itflee.com]      // [...] cannot be changed

User logon name (pre-Windows 2000):
ITFLEE\     paul.hill       // `paul.hill` is autofill
```
You notice that there is separate logon for **pre-Windows 2000**. This field adapt the user logon name to a format that is acceptable by older server operating system, anything before **Windows 2000**. For example, if a user logon name was longer than 20 characters and it will truncated in the **Windows 2000** logon name. If we had 25 characters up here, it only the first 20 down here (`pre-Windows 2000`). Then click **"Next"**.

On the next screen, we were asked to setup the user's password:
```
Create in: itflee.com/itFless/Administrators

Password:           xxxxxxxx
Confirm password:   xxxxxxxx

[] User must change passowrd at next logon
[] User cannot change password
[] Password never expires
[] Account is disable
```
Since we're creating this account for ourselves, we're going to uncheck **"User must change passwrod at next logon"**. Generally, how a new account creation works is that you'll create the account when an Active Directory using a temporary password. Once you created that account, you'll provide the new user, the person who is going to using the account, the user name, and the temporary password. Since we create the user account for ourselves, we do not need to a tempory password, and we would not want to change it once we login.

When we check this **"User cannot change password" checkbox**, it would not the user to change the password. This is useful for service accounts when they are not using the **MSA**, but 9 times out of 10 you are not going to check this particular checkbox. It make your account less secure, so if securities are concerned, do not check this checkbox.

The **"Password never expires" checkbox** is also useful if you're creating service account and not using a **MSA**. If you create an account with this user interface and you know it's going to be a service account, and it's going to used by an application and not an actually real person. Some people do want to check this on their own accounts, so that they don't have to change password (i.e.) every 90 days, or whatever the policies are for your workplace, if security is certain at all on your workplace, don't check this checkbox.

The **"Account is disabled" checkbox** is a good way to create an account for future use that is not ready to be used yet. So for example, if you're working for in a classroom environment and you know you have students coming in, and there are going to need log into the computers, you might create the account two weeks ahead of time, and just check this checkbox, and make sure the account is disable, so they cannot be used until they get there. When they arrive, and trying to login you need to come back and uncheck this checkbox so that the account is enable and disable to be used.

Now on this password setting screen, click **"Next"** and then click **"Finish"** on the next screen. Back to the Active Directory Users and Computers MMC, we can see that the account (Paul Hill) has been created on the main pane while **"itFlee"** -> **"Administrators"** has been highlighted.

Since this is supposed to be an administrator account, at this point, we can see the type is just a regular user (on the main pane):
```
Name          Type
Paul Hill     User
```
If we double-click on the object "Pual Hill" here, a **"Paul Hill Properties" window** popped up, we can click on the **"Member of" tab**. And we can see that it's just part of the **"Domain Users"**.
```
...
Member of:
Name              Active Directory Domain Services Folder
Domain Users      itflee.com/Users
```
To make this account a domain administrator, we need to add the **"Domain Admins"** membership. The way to do that is by clicking on the **"Add"** button, then a **"Select Groups" little window** popped up. In this window, we just need to type in **"Domain Admins"** in the **"Enter the object names to select (examples):"** field, and then we click **"Check Names"**, and then we can see the "Domain Admins" in the field **underlined**. So if we click **"OK"**. We can see this is now a domain admin user:
```
...
Member of:
Name              Active Directory Domain Services Folder
Domain Admins     itflee.com/Users
Domain Users      itflee.com/Users
```
Now we can set this to **primary group** by clicking the **"Set Primary Group"**. But we can see there says *"There is no need to change Primary group unless you have Macintosh or POSIX-compliant applications"*, which we're not using. So just click **"OK"**. Now we have a user account created.



## Search and Find Users or Any Type of Objects in Active Directory
You will need to pull up a certain user and you'll just get a first name and a last name. Some companies have a hundreds of OUs and a thousand of users. To find a user, you have to click on the little search button (tooltip: Find objects in Active Directory Domain Service) on the **standard tool bar**. Then a **"Find Users, Contacts, and Groups" window** popped up. On this windows, first we have to choose **"Users, Contacts, and Groups"** in the **"Find:"** field, and then choose **"Entire Directory"** in the **"In:"** field. And then we're going to type in the name of the person:
```
Find: [Users, Contacts, and Groups]     In: [Entire Directory]

Users, Contacts, and Groups (tab)
Name:         Paul Hill
Description:  [empty]
```
Click **"Find Now"** then the **"Search results:" field** will appeared on the bottom of **"Find Users, Contacts, and Groups" window**:
```
Search results:
Name              Type            Description
Paul Hill         User
```
You can see that it popped up with our account. 9 times out of 10 that's how you're going to find a user account if you're looking for one.

You could also gun to the **"Advanced" tab** in search on the **"Field"** for a particular user like **"Division"**, **"E-Mail Address"**, **"Fax Number"**, say if they're not coming up with the user name or their first and last name but you happen to know their email address you could go here into user, you can type in **"E-Mail Address"** and say **"paul.hill@itflee.com"**. You can also do an **"Employee ID"**, so 9 times out of 10 you don't need to go into this **"Advanced" field**, just typing in their name and you will be good enough.


- ### Search Users and Reset Passwords
A lot of times when you're searching for users like this, the reason why you'll be doing it is to either **unlock their account or reset their password**. Once you find the user account in the **"Search results:"** field, right-click the account (i.e. Paul Hill) and click **"Reset Password..."**. This is the same as that second window when we created the new user account. We have the **"User must change password at next logon" checkbox** and the **"Unlock the user's account" checkbox**. Important thing to keep in mind here is the **"Account Lockout Status"** on this domain controller. And we can see that my account is **"Unlocked"**. If the account was locked, you'd want to check this **"Unlock the user's account" checkbox** down here. Since it's unlocked there's no need to do it, but it doesn't hurt to go ahead and check it anyways.

Password resets are like one of the most common things that happen when you're working on a domain controller, or your administrating a network, especially if you have a lot of users.


### Check if `paul.hill` in the `Domain Admins` Group
Back to the Active Directory Users and Computers MMC, click on **"itflee.com"** -> **"Users"** on the left pane. On the main pane, we can find the **"Domain Admins"**, this is a security group. When we created our new user account, we added them to this group. If we double-click on this group, then we click **"Members" tab**, we can see that **"Paul Hill"** is a member of the **"Domain Admins"** group.




# Groups and Memberships
We're going to create groups and manage group memberships within **Active Directory Users and Computers**. We're going to a security group in **"itFlee" organizational units** that we've created before. So under **"itFlee" OU**, we have **"Domain Users" OU**, this is where we're going to create the group.



## Creating Group
On the ***left pane*** of **Active Directory Users and Computers MMC**, click **"itflee.com"** -> **"ifFlee"** -> **"Domain Users"**, right-click the **"Domain Users" OU**, and we're going to choose **"New"** -> **"Group"**. A **"New Object - Group"** windows popped up, we're going to call this **"Sales"**:
```
Group name:
Sales

Group name(pre-Windows 2000):
Sales

Group scope             Group type
  Domain local          - Security
- Global                  Distribution
  Universal
```
Then we click **"OK"**.

We can see that the **"pre-Windows 2000"** name has been populated, that's the same as when you created a new user account, it creates a name that it will be compatible with servers older than **Windows Server 2000**, and we have **"Group scope"** and **"Group type"**.

Under the **"Group scope"**, we have three options, **"Domain local"**, **"Global"** and **"Universal"**. Basically, these goes from least accessible to most accessible.

The **"Domain local"** group scope is only usable within the domain it was created and cannot be accessed from another domain even if there is a trust established. So if we created another domain and established a trust between `itflee.com` and let's just say `paulhill.com`, we would not be able to access this `Sales` group from the external domain, which it would be `pualhill.com`.

The **"Global"** group scope is the same as **"Domain local"** except that the group can be accessed from another domain if there is a trust established. So if we built `paulhill.com` and we want to access this group called **"Sales"** within `itflee.com`, we would be able to do that if a trust was established between the two domains.

The **"Universal"** group scope is the same as **"Global"** except that the group can be accessd by other forests that trust your domain as well. So that's a level above just sharing it between domains, you can actually share it between forests.

Most of the time, you'll want to leave the **"Global"** scope selected, and we're going to do it right now.

Under the **"Group type"**, we have two options **"Security"** and **"Distribution"**. **"Security"** is for authentication, and **"Distribution"** is for **email lists**. So if we want to set up a security group, and say only people within the **"Sales"** group can have access to these folders in these files. They can only access these types of computers, these people can or cannot remote desktop into servers, that kind of stuff was what you'd specify with a security group.

The **"Distribution"** group type is only used when you have an **Exchange Server** setup on your network. We can create for example a **"IT Support"** group, we could create this **"Distribution"** group and when we added members to this group, someone could send an email to **"IT Support"**, and the email would be also sent to every member of this group.

So keep in mind that **"Distribution"** is only used for emails. So if you have an Exchange Server, you could use a **"Distribution"** group. And **"Security"** is used for authentication and 9 times out of 10 you're going to be going with the **"Security"** option.

Back to the Active Directory Users and Computers MMC, if we go inside of this **OU** (by clicking **"itflee.com"** -> **"itFlee"** -> **"Domain Users"** on left pane), we can see the **"Sales"** group has been created (on the main pane), it's a **"Security Group"** and it's a **"Global"** group:
```
Name            Type
Sales           Security Group - Global
```
If we right click on the group, we can choose **"Properties"** (click it). A **"Sales Properties" window** popped up, we can add a description and email address, **we can even expand the scope but we cannot shrink it**. Also, we can change the group type from **"Security"** to **"Distribution"** if we would like. And we can enter a note.

The two most important tabs here (**"Sales Properties" window**) are the **"Members"** and **"Member Of"** tab. Under the **"Members" tab**, we can add people to the group to make them a member of this group. For example, we're going to add `paul.hill` account by clicking the **"Add..."** button. A **"Select Users, Contacts, Computers, Service Accounts, or Groups" window** popped up, and we're going to type in **"Paul Hill"**, and then we're going to click **"Check Names"** button. We can see that it was able to find our name, it underlined the account here so that means it has successfully resolved the account name. So if we click **"OK"**, back to the **"Sales Properties" window**, we could see that we have been added to the group:
```
Members:
Name            Active Directory Domain Services Folder
Paul Hill       itflee.com/itFlee/Administrators
```
We can click **"Apply"**, and now those changes now take effect.

The **"Member Of" tab** is also important, **we can make this group a member of another group**. Under this tab on the **"Sales Properties" window**, click on **"Add..."** button. A **"Select Groups" window** popped up, and just say we type in **"Administrators"** in the **"Enter the object names to select (examples):"** field and click **"Check Names"** button. We can see it was able to find the **"Administrators"** (underlined) and click **"OK"**.

Back to **"Memeber Of" tab** of the **"Sales Properties" window**, we can see this group **"Sales"** is a member of the **"Administrators"** group:
```
Member of:
Name                Active Directory Domain Service Folder
Administrators      itflee.com/Builtin
```
If we click **"Apply"** button, anyone who is member of this **"Sales"** group is also a member of the **"Administrators"** group. So everyone that we added to this **"Sales"** group will also have the same privileges and the same right as the **"Administrators"** group because this group is also a member of the **"Administrators"** group. Click **"OK"**.

Let's look at this more closely and help you understand what's going on. Back to the Active Directory Users and Computers MMC, on the ***left pane***, click **"itflee.com"** -> **"Builtin"**. On the ***main pane***, double-click on this **"Administrators"** Security Group right here. An **"Administrators Properties"** window popped up, we're going to find a **"Salse"** group is listed here (**"Members"** tab):
```
Members:
Name                Active Directory Domain Services Folder
Administrator       itflee.com/Users
Domain Admins       itflee.com/Users
Enterprise Admins   itflee.com/Users
Sales               itflee.com/itFlee/Domain Users
```
We double-click on this **"Sales"**. A **"Sales Properties"** window popped up, now we're looking at the **"Sales"** group. If we open up the **"Sales"** group member (by clicking **"Members" tab**), we can see that **"Paul Hill"** is here:
```
Members:
Name        Active Directory Domain Services Folder
Paul Hill   itflee.com/itFlee/Administrators
```
So we're in turn by adding ourselves to the **"Sales"** group, and since the **"Sales"** group is added to the **"Administrators"** group. We're an administrator. 

Now we remove the **"Sales"** group from the **"Administrators"** group since it's just for demonstration (by clicking on **"Remove"** button on the **"Members"** tab of the **"Administrators Properties"** window).

Back to the Active Directory Users and Computers MMC, on the left pane, click on **"itflee.com"** -> **"itFlee"** -> **"Domain Users"**. We're just going to go back to the **"Sales"** group and we can delete the group by right-clicking on the group (on the main pane), and just choosing **"Delete"**.


