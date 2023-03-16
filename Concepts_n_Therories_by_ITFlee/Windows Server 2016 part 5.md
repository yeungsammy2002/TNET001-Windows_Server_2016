# Windows Server 2016 - part 5




# Configuring Personal Home Folders for AD User Accounts
We're going to configure home folders for Active Directory user accounts. Home folders and my documents make it easier for an administrator to backup user's files and manage user accounts by collecting the user's files in one location. If you assign a home folder to a user, you can store the user data in a central location on a server, and make backup and recovery of data easier and more reliable.


- ### Create Folder and Set
Let's create a folder in `C:\` called `Home_Folders`.


- ### Set the Folder to Collection of User Folders
Next we need to share the folder so we can make it available on the network. To do that, just right-click the **`Home_Folders` icon** -> click **"Properties"**. 

A **"Home_Folders Properties" window** popped up. Then click on **"Sharing" tab** -> **"Advanced Sharing..."**.

A **"Advanced Sharing" window** popped up. Then check **"Share this folder" checkbox**. Next you need to choose the name of the share, you can use the default name `Home_Folders`. We'd like to give the root folder hidden by putting the `$` sign at the end of the share name:
```
...
Share name:
Home_Folders$
...
```
Then on the same window, click on the **"Permissions" button**.

A **"Permissions for Home_Folders$" window** popped up. Let's check **"Full Control" checkbox**. So now, everyone have a full control:
```
Group or user names:
Everyone

Permissions for Everyone        Allow   Deny
Full Control                    [v]     []
Change                          [v]     []
Read                            [v]     []
```
Click **"Apply"**, then click **"OK"**.

Back to **"Advanced Sharing" window**, click **"Apply"**, then click **"OK"**.

Now we need to set the file permission. Back to **"Home_Folders Properties" window**, click on **"Security" tab**. Then click on **"Advanced" button**.

An **"Advanced Security Settings for Home_Folders" window** popped up. We need to remove inheritance permission, because as you can see, ***domain users*** have a **"Read & execute"**, as well as they have some kind of **"Special"** permission (the **last two rows**). The will be inherited on Administrators's `Home_Folders` and we don't want that. So let's click on **"Disable inheritance"**.

```
...
Permission entries:
Type    Principal                       Access          Inherited from      Applies to
Allow   Administrators(ABC\Admi...)     Full control    None                This folder only
Allow   Administrators(ABC\Admi...)     Full control    C:\                 This folder, subfolders and files
Allow   SYSTEM                          Full control    C:\                 This folder, subfolders and files
Allow   CREATOR OWNER                   Full control    C:\                 Subfolders and files only
Allow   Users(ABC\Users)                Read & execute  C:\                 This folder, subfolders and files
Allow   Users(ABC\Users)                Special         C:\                 This folder and subfolders

Add     Remove      View
Disable inheritance
...
```

A **"Block Inheritance" dialog box**, and there are two options:
1. Convert inherited permissions into explicit permissions on this object.
2. Remove all inherited permissions from this object.

Click on the **first option**.

The **"Permission entries:" field** in the **"Advanced Security Settings for Home_Folders" window** will look like this:
```
...
Permission entries:
Type    Principal                       Access          Inherited from      Applies to
Allow   Administrators(ABC\Admi...)     Full control    None                This folder, subfolders and files
Allow   SYSTEM                          Full control    None                This folder, subfolders and files
Allow   CREATOR OWNER                   Full control    None                Subfolders and files only
Allow   Users(ABC\Users)                Read & execute  None                This folder, subfolders and files
Allow   Users(ABC\Users)                Special         None                This folder and subfolders

Add     Remove      View
Enable inheritance
...
```

Now let's select "Users" (in second to last row) and then click **"Remove"**. Then select the last row's **"Users"**, and then click **"Remove"**. The **"Permission entries:" field** in the **"Advanced Security Settings for Home_Folders" window** will look like this:
```
...
Permission entries:
Type    Principal                       Access          Inherited from      Applies to
Allow   Administrators(ABC\Admi...)     Full control    None                This folder, subfolders and files
Allow   SYSTEM                          Full control    None                This folder, subfolders and files
Allow   CREATOR OWNER                   Full control    None                Subfolders and files only

Add     Remove      View
Enable inheritance
...
```
Click on **"Apply"**, then click **"OK"**.

Back to the **"Permissions for Home_Folders$" window**, click on the **"Sharing" tab**, highlight the **"Network Path:"** then copy it:
```
...
Network Path:
\\OSCAR\Home_Folders$           // copy it
...
```
Then click on **"Close"**.

So we have successfully created a share folder for `Home_Folder` storage location.


- ### Set User Accessible to the Folder
Open **"Server Manager" window**, on the top right menu bar, click **"Tools"** -> **"Active Directory Users and Computers"**.

Active Directory Users and Computers MMC popped up, on the ***left pane***, click **"abc.com" domain** -> **"abc" OU** -> **"Office" OU**. On the main pane, you can see the list of the users like this:
```
Name                Type        Description
Clyde Braiden       User        [empty]
Jolyon Clifton      User        [empty]
Kelsey Mason        User        [empty]
Mike Terry          User        [empty]
Rollo Braith        User        [empty]
```
Highlight all of them, then right-click the highlighted part -> click **"Properties"**.

A **"Properties for Multiple Items" window** popped up, click on **"Profile" tab**, then check **"Home folder" checkbox** and select **"Connect:" radio button**. Then set it to **"H:"** and paste the path `[collection_path]` + `\%username%` to the **"To:"** field like this for example:
```
- Connect:  H:  To: \\OSCAR\Home_Folders$\%username%
```
`%username%` is a variable for user logon name. Click on **"Apply"**, and then click **"OK"** to close the window.

Back to Active Directory Users and Computers MMC, on the ***left pane***, click **"abc.com" domain** -> **"abc" OU** -> **"Office" OU**. On the main pane, select one of the users, for example, `Mike Terry` and then right-click on it -> click **"Properties"**.

A **"Mike Terry Properties" window** popped, click on **"Profile" tab**, you can see something like this:
```
- Connect:  H:  To: \\OSCAR\Home_Folders$\Mike Terry
```

Now back to the desktop, open the folder explorer. Find the folder `C:\Home_Folders`, you should see a bunch of folders that named using the `Office` OU's users:
```
This PC > Local Disk (C:) > Home_Folders
Clyde Braiden
Jolyon Clifton
Kelsey Mason
Mike Terry
Rollo Braith
```
To check if `Mike Terry` is taking the full control of the folder, right-click `Mike Terry` folder -> click **"Properties"**.

A **"Mike Terry Properties"** window popped up, click on **"Security" tab**, in the **"Group or user name:" field**, click **"Mike Terry (Mike Terry)"**. You can see something like this in the **"Permissions for Mike Terry" field**:
```
Permissions for Mike Terry      Allow       Deny
Full Control                    v
Modify                          v
Read & execute                  v
List folder contents            v
Read                            v
Write                           v
```
The **`Administrator (ABC\Administrators)`** has the same permissions as well.


- ### Access the Folder from Client Computer
In a client computer, let's login with the `Mike Terry` account. On the desktop, open the Folder Explorer, on the ***left pane***, click on **"This PC"**, you should see the share folder appeared on the **"Network locations"** section by default.




