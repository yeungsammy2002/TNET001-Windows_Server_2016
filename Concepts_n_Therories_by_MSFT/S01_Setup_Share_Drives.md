# Section 01 - Setting Up Share Drives



## Creating Folder and Setting Up Share Drive
To create a share drive that include the domain in the share drive path, you need to follow these steps:

1. Create a folder that is going to be the share drive.

2. Right-click on the folder and select **"Properties"** from the context menu.

3. Click on the **"Sharing"** tab in the **"Properties"** window.

4. Click the **"Advanced Sharing"** button.

5. Check the box next to **"Share this folder"** to enable sharing.

6. Enter a new share if needed.

7. Click the **"Permissions"** button.

8. Click the **"Add"** button to add the domain user or group that you want to grant access to the folder.

9. Click the **"Object Types"** button.

10. Check the **"Groups"** box and click **"OK"**.

11. Enter domain name followed by backslash () and the group name, for example, `DOMAIN\Group`, in the **"Enter the object names to select"** field.

12. Click **"Check Names"** to verify the enter domain group name.

13. Click **"OK"** to add the domain group to the share permissions list.

14. In the **"Permissions"** window, select the domain group you just added.

15. Choose the access level you want to grant to the selected domain group, such as **"Read"** or **"Full Control"**.

16. Click **"OK"** to apply the changes and close the **"Permissions"** window.

17. Click **"OK"** to apply the changes and close the **"Advanced Sharing"** window.

18. Close the **"Properties"** window.

The share drive path will now include the domain when accessed by the domain users, for example, `\DOMAIN\ShareName`.



## 

