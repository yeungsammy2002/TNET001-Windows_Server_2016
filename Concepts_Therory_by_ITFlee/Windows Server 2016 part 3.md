# Windows Server 2016 - part 3




# Group Policy
***Group Policy*** is a tool used by system administrators to quickly and easily make a configuration changes to users and computers within Active Directory. With Group Policy, you can implement security configurations across your domain quickly and easily, you can do things like restrict certain users from logging into the certain computers, allow only certain users to access certain files, give specific users or all users a specific desktop background, or deploy software to your domain workstations.

***Group Policy*** is a must-have skill if you want to be a ***Windows Server administrator***, or a system administrator. Keep in mind that you cannot understand Group Policy without understanding Active Directory.


## Group Policy Objects
Group Policy works by applying ***Group Policy Object* (a.k.a *GPO*)** to the **OU** structure that you've created in Active Directory. A Group Policy Objects contains configuration settings for both users and computers. When a ***GPO*** is applied to an **OU**, the settings configure in the ***GPO*** are applied to users and computers that are within that **OU**. You can also configure ***GPOs*** to only apply to a certain objects by defining the security filtering. The most common and default choice is authenticated users group, which is basically any valid user and computer within Active Directory.

***GPOs*** are applied **recursively**. This means that the settings will also be applied to all **sub-OUs**, beneath the **original OU** that the ***GPO*** was applied to.

To start Group Policy, you need to open **"Server Manager"**, on the top right menu bar, select **"Tools"** -> **"Group Policy Management"**. An Group Policy Management MMC will be popped up. On the left pane of the MMC, expand **"Forest: itflee.com"** by clicking the **">"**:
```
Group Policy Management
    Forest: itflee.com
      > Domains
      > Sites
        Group Policy Modeling
        Group Policy Results
```
Now you will see **"Domains"**, **"Sites"**, **"Group Policy Modeling"** and **"Group Policy Results"**.

The **"Domains"** folder contains all the domains that are underneath the forest.

The **"Sites"** folder contains all the sites that you may have configured to Active Directory site and services. In short, this is used when you have servers that are physically in a different locations, like a differnt building, city, or even a country.

The **Group Policy Modeling** and **"Group Policy Results"** are both tools that can be used to trouble shoot issues with Group Policy.

Let's expand the **"Domains"** folder, and then expand the **"itflee.com"**:
```
Group Policy Management
    Forest: itflee.com
        Domains
            itflee.com
                Default Domain Policy (link)
              > Domain Controllers
              > itFlee
              > Group Policy Objects
              > WMI Filters
              > Starter GPOs
        Sites
        Group Policy Modeling
        Group Policy Results
```
From this view, you can see a similar view to that in Active Directory. Note that you cannot see any of the Active Directory containers, like **"Users"** for example, but we can see the **OU** that we have created and we can see the **"Domain Controllers" OU**.

Directly beneath the **"itflee.com"**, we have the **"Default Domain Policy"**. As the name implies, this **GPO** comes by default when a new domain is created. Since it directly underneath the domain, it will apply to all the Active Directory objects beneath the root domain. So this **GPO** not only applies to everything at the root level here, but everything in our **"itFlee" OU**, everything in our **"Administrators" OU** and our **"Domain Users" OU**:
```
Group Policy Management
    Forest: itflee.com
        Domains
            itflee.com
                Default Domain Policy (link)
              > Domain Controllers
                itFlee
                    Administrators
                    Domain Users
              > Group Policy Objects
              > WMI Filters
              > Starter GPOs
        Sites
        Group Policy Modeling
        Group Policy Results
```
Notice that we cannot see actual Active Directory objects, so we can't see users in this view (by clicking the **"Administrators" OU** on left ***pane*** then view the ***main pane***). We can only see the Group Policy Objects that have been applied to this **OUs**, which right now is just the **"Default Domain Policy"**.

The **"Group Policy Objects"** folder contains all the **GPOs** that are inside your domain whether they are currently in use or not. So here we can see the **"Default Domain Controllers Policy"** and the **"Default Domain Policy"** are listed. If you expand the **"Domain Controllers" OU**, we can see that GPO **"Default Domain Controllers Policy"** is listed here:
```
Group Policy Management
    Forest: itflee.com
        Domains
            itflee.com
                Default Domain Policy (link)
                Domain Controllers
                    Default Domain Controllers Policy (link)
                itFlee
                    Administrators
                    Domain Users
              > Group Policy Objects
              > WMI Filters
              > Starter GPOs
        Sites
        Group Policy Modeling
        Group Policy Results
```
And again, this **"Group Policy Objects"** folder is just a list of every single **GPO** that you have in your domain. Even if it wasn't in use, it was still be listed here.

The **"WMI Filters"** folder allows you to add specific rules of when a specific **GPO** should be applied on not. For example, you can only apply a particular GPO if the computer was using an operating system of **Windows 7** or newer.

The **"Starter GPOs"** folder is used when you want to import or export for **GPO** for distributions to other environments.




# Creating and Managing Group Policy Objects (GPOs)
GPOs contains settings and configurations that can be applied to users or computers that are stored in Active Directory.

A domain can contain several **GPOs**, and you'll always never see a domain that contains only one **GPO**. It's also important to understand that one individual **GPO** can be linked or applied to all multiple **OUs** simultaneously.



## Link Existing GPO to Existing OU
By expanding the **"Group Policy Objects"** folder on the ***left pane***, we can see that we have the **"Default Domain Controllers Policy"** and the **"Default Domain Policy"**:
```
Group Policy Management
    Forest: itflee.com
        Domains
            itflee.com
                Default Domain Policy (link)
                Domain Controllers
                    Default Domain Controllers Policy (link)
              > itFlee
                Group Policy Objects
                    Default Domain Controllers Policy
                    Default Domain Policy
              > WMI Filters
              > Starter GPOs
        Sites
        Group Policy Modeling
        Group Policy Results
```
Let's say we want to link the **"Default Domain Controllers Policy"** to this **"itFlee" OU**. The way to do that is right-click on the **"itFlee" OU**, and choose the **"Link an Existing GPO..."**. A **"Select GPO" window** popped up, and then (int the **"Group Policy objects:"** field) we would select the **"Default Domain Controllers Policy"**:
```
Select GPO
    Look in this domain:
        itflee.com
    Group Policy objects:
        Name
        Default Domain Controllers Policy       // select this
        Default Domain Policy
```
And then we just click **"OK"**.

Back to the Group Policy Management MMC, now we can see the **"Default Domain Controllers Policy" GPO** apply to the **"itFlee" OU** and the **"Domain Controllers" OU**:
```
Group Policy Management
    Forest: itflee.com
        Domains
            itflee.com
                Default Domain Policy (link)
                Domain Controllers
                    Default Domain Controllers Policy (link)
                itFlee
                    Default Domain Controllers Policy (link)
                    Administrators
                    Domain Users
                Group Policy Objects
                    Default Domain Controllers Policy
                    Default Domain Policy
              > WMI Filters
              > Starter GPOs
        Sites
        Group Policy Modeling
        Group Policy Results
```
If we're going to **"Group Policy Objects" folder**, look at the ***main pane***, we're still only have the two **GPOs** created, but they have been linked in more than one spot:
```
Name                                    GPO Status      WMI Filter      Modified        Owner
Default Domain Controllers Policy       Enabled         None            5/13/2017..     Domain Admin(ITFLEE)
Default Domain Policy                   Enabled         None            5/17/2017..     Domain Admin(ITFLEE)
```
Just to delete that link, we can right-click on it (Forest: itflee.com -> Domains -> itflee.com -> itFlee -> Default Domain Controllers Policy), and choose **"Delete"**. A dialog popped up and says ***"Do you want to delete this link? This will not delete the GPO itself"***, we'd click **"OK"**. Now that link has been deleted but if we go under the **"Group Policy Objects"** folder, we can still see the **GPO** is still in the domain:
```
Group Policy Management
    Forest: itflee.com
        Domains
            itflee.com
                Default Domain Policy (link)
                Domain Controllers
                    Default Domain Controllers Policy (link)
                itFlee
                    Administrators
                    Domain Users
                Group Policy Objects
                    Default Domain Controllers Policy
                    Default Domain Policy
              > WMI Filters
              > Starter GPOs
        Sites
        Group Policy Modeling
        Group Policy Results
```
**GPOs** are used in a modular sense, meansing that an administrator might create several **GPOs** and apply them to **OUs** as needed. For example, you could create a **GPO** that installs ***Flash Player*** that contain computers which would need ***Adobe Flash Player*** installed. Or you could create a **GPO** that prevents users from launching ***Internet Explorer***, and you could link that ***GPO*** to all the ***OUs*** where you don't want users to be able to run ***Internet Explore***.

Creating ***GPO*** is very similar to create a user account or an organizational unit in Active Directory. You simply need to right-click on the domain or **OU** and choose create a ***GPO*** in this domain and link it here.

So if we wanted to create a ***GPO*** under the root of our domain, we would right-click on **"itflee.com"** on the ***left pane***, and then click **"Create a GPO in this domain, and Link it here..."**. A **"New GPO" dialog box** popped up, and we're going to call this **"Test GPO"** (type it in the **"Name:"** field). If we had **Source Starter GPO**, we could select them here (**"Source Starter GPO:"** field), in this case, we don't have any. Then we're just click **"OK"**.

Now we can see the new ***GPO*** has been created and linked to **"itflee.com"**:
```
Group Policy Management
    Forest: itflee.com
        Domains
            itflee.com
                Default Domain Policy (link)
                Test GPO (link)
              > Domain Controllers
              > itFlee
                Group Policy Objects
                    Default Domain Controllers Policy
                    Default Domain Policy
                    Test GPO
              > WMI Filters
              > Starter GPOs
        Sites
        Group Policy Modeling
        Group Policy Results
```
If we go under the **"Group Policy Objects"** (on ***left pane***), we can see that we have 3 Group Policy Objects in our domain.

We can right-click on this ***GPO*** (Forest: itflee.com -> Domains -> itflee.com -> Test GPO (link) on the ***left pane***), there's a number of things we can do:
```
- Edit...
- Enforced
- Link Enabled (checked)
- Save Report...
- New Window from Here
- Delete
- Rename
- Refresh
- Help
```
We can edit the ***GPO***. We can enforce it, meaning it will take precedence over other ***GPOs***. We can uncheck this **"Link Enabled"** option, if we click that, we can see the icon (on the ***left pane***) goes lighter and that means that the ***GPO*** is not going to be applied to this domain or anywhere at all, it's still linked to it but none of the settings will take effect. We'll right-click **"Test GPO"** (link), and choose **"Link Enable"** again to enable it again.



## Save Report
We can save a report of the ***GPO***. You can see that by right-clicking **"Forest:itflee.com"** -> **"Domains"** -> **"itflee.com"** -> **"Default Domain Policy" (link)**, and then choose **"Save Report..."**. And we can save it to the desktop (in **HTML** format). If we go to our desktop, you can open this **"Default Domain Policy" HTML file**. Now we can see there is a report displaying all the configuration settings of our default domain policy. That is the same as clicking on the (**"Forest:itflee.com"** -> **"Domains"** -> **"itflee.com"** -> **"Default Domain Policy" (link)** on the ***left pane***) ***GPO*** and clicking on **"Settings" tab** (on the ***main pane***). Now we can see here that it's opening ***Internet Explorer*** warning dialog box saying something like *Do you trust this website...*, we're going to hit the **"Close"** button. And we can see the exact same settings here (**"Settings"** tab on ***main pane***) as well. So you don't have to save a report if you want to view the settings.

If we'd like, we can make additional changes to the view (by right-clicking **"Forest:itflee.com"** -> **"Domains"** -> **"itflee.com"** -> **"Default Domain Policy" (link)**, and then click **"View"** -> **"Options"**), we can make additional changes to the view, we can change some of the columns, reporting and just some general settings if we would like.

You can create a new view from here (by right-clicking **"Forest:itflee.com"** -> **"Domains"** -> **"itflee.com"** -> **"Default Domain Policy" (link)**, and then click **"New Window from Here"**). A new Group Policy Management MMC popped up, on the ***left pane***, it only show that ***GPO*** (on the ***left pane***) and it gives you the same exact set of option, it gives you the same exact set of options overhere (on the ***main pane***). So to get out of this view, you just click the little `x` up here (right side of standard menu). Now we returned to a much more functional view.



## Delete, Rename, Refresh GPO Link & get Help
We can also delete the ***GPO*** link (by right-clicking the ***GPO*** link). Note that we're not deleting the ***GPO*** because we're clicking on a link, not the ***GPO*** itself. We can rename, refresh, and we get help, but 9 times out of 10 if you need help you can go on ***Google***.



## Settings inside of GPO
Let's right-click on the **"Forest:itflee.com"** -> **"Domains"** -> **"itflee.com"** -> **"Test GPO" (link)**, and choose **"Edit.."**. A Group Policy Management Editor MMC will appear, and this is where you can make your configuration changes to your GPO.

In this MMC, we see we have two types of configuration - computer and user (on the ***left pane***):
```
Test GPO [ITFDC01.ITFLEE.COM]
Computer Configuration
    > Policies
    > Preferences
User Configuration
    > Policies
    > Preferences
```
**"Computer Configuration"** will only be applied to **computer objects**, and the **"User Configuration"** will only be applied to **user objects** within Active Directory. So if this **GPO** is applied to an **OU** that only contains computers and you make changes under the **"User Configuration"**, none of the settings will be applied to those objects. The same goes for computers, if you apply this **GPO** to an **OU** that only contains users, and you changes under the **"Computer Configuration"**, none of the settings will be applied to those user accounts.

Understanding the difference between these two configurations are extremely important, we see a lot of system administrators make changes under the **"Computer Configuration"** like setting a *desktop background*, and then they link the **GPO** to an **OU** that only contains user accounts. This will **NOT** work.



## Delete GPO
Back to the Group Policy Management MMC, on the ***left pane***, expand **"Group Policy Objects"** like this:
```
Group Policy Management
    Forest: itflee.com
        Domains
            itflee.com
                Default Domain Policy (link)
                Test GPO (link)
              > Domain Controllers
              > itFlee
                Group Policy Objects
                    Default Domain Controllers Policy
                    Default Domain Policy
                    Test GPO
              > WMI Filters
              > Starter GPOs
        Sites
        Group Policy Modeling
        Group Policy Results
```
We can see that the **"Test GPO"** is listed here (**"Group Policy Objects"**). If we right-click on this **"Test GPO"**, we can choose **"Delete"**. A dialog box popped up and says ***"Do you want to delete this GPO and all links to it in this domain? This will not delete links in other domains."***, we click **"Yes"**. We can see that all the links has been deleted as will as in the **"Group Policy Objects"** folder. So that **GPO** has been deleted.




# Group Policy Precedence
**"Precedence"** means the order or the way that things are done. With Group Policy, there is a specific order in which Group Policy Objects or GP settings are applied. It's important to understand this, because from time to time, you'll have multiple ***GPOs*** trying to configure the same setting and you have to understand the precedence in order to understand which settings will be applied and which settings will be ignored.

You can remember this order by remembering the acronym, **LSDOE**, stands for ***Local***, ***Site***, ***Domain***, ***OU*** and ***Enforced***:
1. Local GP... `gpedit.msc`     (least important)
2. Site
3. Domain
4. Organizational Unit
    - Sub Organizational Unit (if any)
5. Enforced Group Policy Objects


The order that Group Policy runs is starting with the **local Group Policy**. If you hit the **Windows** button and type in `gpedit.msc`. You will be able to edit the local Group Policy. Now this is the first thing that is applied to the computer and it's also viewed as the least important. 

Next, any Group Policy Objects that are assigned to your site are then applied, and this means that it overrides any conflicts that it may find between the local and the **"Site"** Group Policy. So if you configure a desktop wallpaper in the local Group Policy and you configure it in the **"Site"** policy, the **"Site"** policy will take precedence over the local Group Policy because it was applied after the local Group Policy.

Next in the order is the **"Domain"** policy, so any policies assigned to the domain will now be applied on top of the **"Site"** and local settings.

Next, we have the **"Organizational unit"**, and this is any **GPO** that is linked to a specific **OU**, also that goes for **sub-OU**, so if there's an organizational unit within and organizational unit, the **sub-OU** will be applied last and therefore its settings will take precedence over anything that is above it.

Finally, we have **"Enforced Group Policy Objects"**. This is any **GPO** where you've right-clicked and choose to enforce the **GPO**.

To recap, you start with local that's the least important **GPO**, because it's the first one that is computed. You end with **"Enforced Group Policy Objects"**, so if they're conflicting settings between the local and the enforced, since the **"Enforced Group Policy Objects"** will be run last, they will take precedence. So remember the last **GPO** to be applied always wins.



## Blocked Inheritance
Within Group Policy, there's something called ***blocked inheritance***, and this is a term that is used when it comes to organizational units. **OU** can block its inheritance which means only **GPOs** inside of that **OU** will apply except for **Enforced GPOs** that are above the **OU**. Now for block inheritance, you simply right-click on the **"itFlee" OU**:
```
Group Policy Management
    Forest: itflee.com
        Domains
            itflee.com
                Default Domain Policy (link)
                Test GPO (link)
              > Domain Controllers
              > itFlee                  // right-click -> Block Inheritance
              > Group Policy Objects
              > WMI Filters
              > Starter GPOs
        Sites
        Group Policy Modeling
        Group Policy Results
```
You can choose **"Block Inheritance"**:
```
Create a GPO in this domain, and Link it here...
Link an Existing GPO...
Block Inheritance
Group Policy Update...
...
```
On this particular circumstance, if you want to block inheritance from this **"itFlee" OU**. The **"Default Domain Policy"** would **NOT** apply, but **"Test GPO"** would apply.

Let's take another example:
| Policies | Desktop Background GPO link |
| - | - |
| `itflee.com` (Domain Policies) | `itflee.jpg` X |
| `itFlee` (OU Policies) |  `itlogo.jpg` X |
| `Administrators` (Sub OU Policies) | `pauliscool.jpg` (using) |

Let's say in `itflee.com`, we have `itflee.jpg` configured. In **OU**, we have `itflogo.jpg`. And then we have `pauliscool.jpg` under **"Administrators"**. We can see that represented down here:
```
Group Policy Management
    Forest: itflee.com
        Domains
            itflee.com
                Default Domain Policy (link)
                itflee.jpg (link)
              > Domain Controllers
                itFlee
                    itflogo.jpg (link)
                    Test GPO (link)
                    Administrators (!)
                        pauliscool.jpg (link)
                ...
```
The Group Policy Objects are actually called `itflee.jpg`, we have name them what the actual desktop background filename is. In this particular scenario, we have `itflee.jpg (link)` linked to `itflee.com (domain)`. And we have `itflogo.jpg (link)` linked to `itFlee (OU)`. And then on `Administrators`, we have `pauliscool.jpg (link)` and we can see that's referenced right here.

Since we're going down to a **Sub OU** `pauliscool.jpg (link)` will win, because we have ***Local***, ***Site***, ***Domain***, ***OU*** and ***Enforced***. Let's say we've blocked inheritance, that means the `itflee.jpg (link)` still is not going to apply, the `itflogo.jpg (link)` is not going to apply (blocked from here), and `pauliscool.jpg (link)` is still going to apply. So nothing really change except `Test GPO (link)` and `Default Domain Policy (link)` now **NO** longer applied to the **"Administrators" OU**. There is an **exclamation mark** in the **"Administrators" OU icon** because it is blocking the inheritance.

What if we enforce the `itflee.jpg (link)`, you can see that here that the `iflfee.jpg (link)` icon is changed. This is the icon when you see it's locked, that means the **GPO enforced**, and when you see this **exclamation** that means the **GPO** is blocking inheritance:
```
Group Policy Management
    Forest: itflee.com
        Domains
            itflee.com
                Default Domain Policy (link)
                itflee.jpg (link)(locked)
              > Domain Controllers
                itFlee
                    itflogo.jpg (link)
                    Test GPO (link)
                    Administrators (!)
                        pauliscool.jpg (link)
                ...
```
In this circumstance, `itflee.jpg (link)` will take precedence, because it is an **enforced GPO**. Remember, we have ***Local***, ***Site***, ***Domain***, ***OU*** and ***Enforced***. So ***Enforced*** always win overall of those:
| Policies | Desktop Background GPO link |
| - | - |
| `itflee.com` (Domain Policies) | `itflee.jpg` (enforced) |
| `itFlee` (OU Policies) |  `itlogo.jpg` X |
| `Administrators` (Sub OU Policies) | `pauliscool.jpg` x |




## Computer vs User
Within a **GPO**, you have a **Computer and a User Configuration**. The **Computer Configuration** is applied first and the **User Configuration** is applied second. We said that the settings that are applied last are the ones that are going to win. So if you have conflicting settings between your **Computer and User Configuration**, the **User Configuration** will win that battle. So the **Computer Configuration** is the least important and the **User Configuration** is the most important.

In this Group Policy Management Editor MMC, you can see at the top you have the **Computer Configuration**, and the **User Configuration**:
```
Test GPO [ITFDC01.ITFLEE.COM]
Computer Configuration
    > Policies
    > Preferences
User Configuration
    > Policies
    > Preferences
```



