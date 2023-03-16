# Windows Server 2016 - part 4




# Storing User Input into Variables using `Windows PowerShell ISE`
We're going to use ***PowerShell*** to create user accounts in Active Directory.

First, you need to log into the domain controller. Open the **"Server Mananger"**, on the top right menu bar of the **"Server Manager" window**, click **"Tools"** -> **"Windows PowerShell ISE"**. We're going to use the 64-bit version (not **x86**) which is the default. The **"Administrator: Windows PowerShell ISE" window with PowerShell** appeared.

This ***PowerShell*** is a bit like **command prompt**, so you can type in a command like `ipconfig` and stuff like that. But if you want to write a script, in this window, the first we need to do is click the **"Script" drop down button** on the **top right corner** of the ***PowerShell***.



## Basic PowerShell Script for Windows
Note that PowerShell script in Windows is using `.ps1` extension, which is a plain text that contains one or more PowerShell commands. Running a script is a lot like running `cmdlet`.


- ### Comments: `#`
Any statement starting with `#` sign consider a **comment**. It help you understand code, it is going to be very helpful when you come back 3 months from now, and you need to make a change to the code you writing. For example:
```
# Store users first name into variable
```


- ### Create Variable: `$`
Any name starting with `$` sign is considered a variable. Then it can be initialized using `=` just like in most programming languages. For example:
```
$firstname = "John"
```



## Pass Information into Active Directory


- ### Import Active Directory Module: `Import-Module ActiveDirectory`
We can pass informations onto Active Directory. To do this, the first thing we want to do is import a module called `ActiveDirectory` by using `Import-Module` command:
```
Import-Module ActiveDirectory
```
Beware that if you're not on a domain controller, you're going to get error at this point. If you are, you should see nothing if you **run** this:
```
PS C:\Users\Administrator> Import-Module ActiveDirectory

PS C:\Users\Administrator> 
```


- ### Create New OU & Find its OU Path
We're going to create a new organizational unit for the ***PowerShell* users**, so we expand `itflee.com` on the ***left pane***, and right-click `itflee.com`. Then click **"New"** -> **"Organizational Unit"**, a **"New Object - Organizational Unit" window** popped up, we're going to call this **"PowerShellUsers"** (in **"Name:"** field), then click **"OK"**.

**OU path** is **NOT** like a file structure where would be like `C:\Users\...` and it is a little bit confusing. To get the **OU path**, open **"Server Manager"**, on the top right menu bar, click **"Tools"** -> **"Active Directory Users and Computers"**. A Active Directory Users and Computers MMC appeared, we need to turn on the advanced view. So on the **Standard menu**, click on **"View"** -> **"Advanced Features"**.

To find the path to this **OU**, we need to right-click on it **`PowerShellUsers` OU** and choose **"Properties"**. A **"PowerShellUsers Properties" window** popped up, click on **"Attribute Editor" tab**. On the **"Attributes:" field**, you can see there is an attribute called **"distinguishedName"**. If you double-click on this attribute, a "String Attribute Editor" dialog box popped up, this (**"Value:" field**) is the path that you need to specify in the ***PowerShell***:
```
String Attribute Editor
Attribute:          distinguishedName
Value:
OU=PowerShellUsers,DC=itflee,DC=com     // copy this
```
**(NOT created)** If you create a new **OU** called **"`TestOU`"** inside the **`PowerShellUsers` OU**, you will see something like that in the **"Value:" field**:
```
OU=TestOU,OU=PowerShellUsers,DC=itflee,DC=com
```
So the deeper you go, the further it's on the ***left***.

Back to the **PowerShell scripting editor**. We have to specify the desired **OU** is a required argument for the command. We make a new variable called `$OUpath` and we want to initialize it with the **OU path** we just copied from the Active Directory.
```
$OUpath = "OU=PowerShellUsers,DC=itflee,DC=com"
```


- ### Secure User's Password: `ConvertTo-SecureString`
Let's say we have a variable called `$password` which stored an user's password. We can't just hand the `$password` variable into Active Directory and expected to process it. It needs to be secure by convert the passowrd to a **secure string**. We can do this by using `ConvertTo-SecureString` command:
```
$password = "abc@1234"
$securePassword = ConvertTo-SecureString $password -AsPlainText -Force
```
The `-AsPlainText` and `-Force` option will make sure that it goes through without any issues. If not a secure string, it will not work.


- ### Create User Account in Active Directory: `Newe-ADUser`
We can create user account in Active Directory and we would like to force the users to change their passwords when logon at the first time by themselves.

We can do this by using `New-ADUser` command. This command has a bunch of arguments that you're going to need to specify. To start, we're going to specify the name by using `-Name` option, then the given name by using `-GivenName` option, then the sur name by using `-Surname`, then the user name that you're going to login with by using `-UserPrincipalName` option, then the **OU path** by using `-Path` option, then the secure string by using `-AccountPassword` option, then the change password at the first log on by using `-ChangePasswordAtLogon` option, and the set the account to enable by using `-Enable` option:
```
New-ADUser -Name "$firstname $lastname" -GivenName $firstname -Surname $lastname -UserPrincipalName "$firstname.$lastname" -Path $OUpath -AccountPassword $securePassword -ChangePasswordAtLogon $true -Enable $true
```
Note that only a string that contains `space` or combining two variables has to be wrapped with ***double quotes* `""`**. When you want to set ***true*** to the `-ChangePasswordAtLogon` and the `Enable` option, you have to provide `$true`.

When we run this, if we don't get some error messages, that means we should created an user account in Active Directory successfully. Here is the output on the ***PowerShell***:
```
PS C:\Users\Administrator> $firstname = "Paul"
$lastname = "Hill"
$password = "ABC@1234"
$securePassword = ConvertTo-SecureString $password -AsPlainText -Force
$OUpath = "OU=PowerShellUsers,DC=abc,DC=com"

New-ADUser -Name "$firstname $lastname" -GivenName $firstname -Surname $lastname -UserPrincipalName "$firstname.$lastname" -Path $OUpath -AccountPassword $securePassword -ChangePasswordAtLogon $true -Enabled $true

PS C:\Users\Administrator> 
```
Now you should a new user account called `Paul Hill` inside the **"PowerShellUsers" OU** in the Active Directory Users and Computer window.


- ### Save PowerShell Script
On the Standard menu of the Administrator: Windows PowerShell ISE window, click **"File"** -> **"Save As..."**. A **"Save As"** window popped up, we can save it to the desktop. Let's say we're going to call it `CreateUseraccounts`, and click **"Save"**. Now we can see the `CreateUseraccounts.ps1` file on the desktop, we can right-click on this ***PowerShell script*** and then click **"Run with PowerShell"** to execute the script.



## Other Useful PowerShell Commands


- ### Get Users Input by Prompting: `Read-Host -Prompt` & Output Information: `echo`
By using `Read-Host` command, the user is going to be asked to put in some kind of the input. Then we can add a prompt by putting `-Prompt` option and provide some kind of prompt in quotation marks:
```
# Output the users information
$firstname = Read-Host -Prompt "Please enter your first name"
$lastname = Read-Host -Prompt "Please enter your last name"
echo "Your full name is $firstname $lastname"
```
Note that if you typed a word that the PowerShell recognized, you can press `tab` to auto-complete the word. For example, type `R`, then something like a tooltip popped-up, when `Read-Host` highlighted, just press `tab` to auto-complete the whole word.

When we click **"Play" icon** above the ***PowerShell***, we can see the prompt in the ***PowerShell***:
```
PS C:\Users\Administrator> # Output the users information
$firstname = Read-Host -Prompt "Please enter your first name"
$lastname = Read-Host -Prompt "Please enter your last name"
echo "Your full name is $firstname $lastname"
Please enter your first name: Paul              // let's say you type in `Paul`, then press `Enter`
Please enter your last name: Hill               // type in `Hill`, press `Enter`
Your full name is Paul Hill                     // computer response

PS C:\Users\Administrator> 
```
You can see you the scripts will be displayed on the ***PowerShell*** when you run this.


- ### Create Several User Accounts at Once using `while` loop
Instead of just run the prompt statements over ane over, we can put all the prompt statement into a `while` loop:
```
Import-Module ActiveDirectory

$exit = ""

While($exit -ne "q") {
    # Store users first name into variable
    $firstname = Read-Host -Prompt "Please enter your first name"
    $lastname = Read-Host -Prompt "Please enter your last name"
    $password = "ABC@1234"

    # Output the users information
    echo "Your full name is $firstname $lastname. Your password is $password"

    # Specify where to store the user account
    $OUpath = "OU=PowerShellUsers,DC=itflee,DC=com"

    # Convert the password to a secure string
    $securePassword = ConvertTo-SecureString $password -AsPlainText -Force

    # Create the user account
    New-ADUser -Name "$firstname $lastname" -GivenName $firstname -Surname $lastname -UserPrincipalName "$firstname.$lastname" -Path $OUpath -AccountPassword $securePassword -ChangePasswordAtLogon $true -Enabled $true

    # Exit the loop?
    $exit = Read-Host -Prompt "Type 'q' to stop creating user account."
}
```




# Create User Accounts from CSV Spreadsheet
You can create user accounts with ***PowerShell*** for Active Directory based on **Excel spreadsheet**, or any comma seperated spreedsheet, anything that can export to a `.csv` file type.

Let's say we have this informations in our **Excel spreadsheet** called `accounts.csv`:
| First Name | Last Name | Job Title | Email Address | Organizational Unit |
| - | - | - | - | - | - |
| Mike | Terry | Office Manager | mike.terry@itflee.com | OU=Office,OU=itFlee,DC=itflee,DC=com |
| Ridley | Quin | Software Engineer | ridley.quin@itflee.com | OU=Administrators,OU=itFlee,DC=itflee,DC=com |
| Ridley | Dalton | Network Administrator | ridley.dalton@itflee.com | OU=Administrators,OU=itFlee,DC=itflee,DC=com |
| Rollo | Braith | Technical Analyst | rollo.braith@itflee.com | OU=Office,OU=itFlee,DC=itflee,DC=com |
| Stan | Kenzie | Support Specialist | stan.kenzie@itflee.com | OU=Administrators,OU=itFlee,DC=itflee,DC=com |
| Clyde | Braiden | Data Analyst | clyde.braiden@itflee.com | OU=Office,OU=itFlee,DC=itflee,DC=com |
| Jolyon | Clifton | Web Developer II | jolyon.clifton@itflee.com | OU=Office,OU=itFlee,DC=itflee,DC=com |
| Kelsey | Mason | Executive Assistant | kelsey.mason@itflee.com | OU=Office,OU=itFlee,DC=itflee,DC=com |
| Conway | Basil | System Administrator I | conway.basil@itflee.com | OU=Administrators,OU=itFlee,DC=itflee,DC=com |
| Earnest | Britton | Support Specialist | earnest.britton@itflee.com | OU=Administrators,OU=itFlee,DC=itflee,DC=com |

Here we have 10 users, and contains information about ***Job Title***, ***Email Address***, ***Organizational Unit***...etc. And also contains the destination organizational unit of where is this user is going to go. These user accounts need to be created, and they need to be put in the appropriate **OUs**. It will take a lot of time to go through Active Directory created a new user account, place some of the appropriate **OU**, entering job title, email address...all that. And doing that with the **GUI** for all 10 of these users. Now imagine if you had about 75 or 100 people that you had to create. You can script this in ***PowerShell*** and make your life much easier.

Keep in mind that we're not going to be saving this as an **Excel spreadsheet file**, we're going to be saving this as **CSV (Comma delimited)**. If you go to `technet.microsoft.com` and you look at the `New-ADUser`, here is a list of everything that you can specify in Active Directory. For example, you can specify the city, company, country, division, employee ID, fax number...etc if you would like.


### 1. Open Administrator: Windows PowerShell ISE
We're going to let the PowerShell script read this ***CSV*** file in ***PowerShell***. First back to **"Server Manager" window**, on the top right menu bar, click **"Tools"** -> **"Window PowerShell ISE"**. An Administrator: Windows PowerShell ISE window popped up, on the top right corner of the PowerShell screen, click the expand **"Script"** icon to open the script editor.


### 2. Write PowerShell Script to Read CSV
```
# Import required modules
Import-Module ActiveDirectory

# Prompt user for CSV file path
$filepath = Read-Host -Prompt "Please enter the path to your CSV file"

# Import the file into a variable
$users = Import-Csv $filepath
```
The first thing we're going to do is to import the `ActiveDirectory` module. 

Then we need to get the file path from the user, so we're going to prompt the user to enter destination or where the file is located that we're trying to open and read by using `Read-Host` command. We're going to assign this to a variable called `$filepath`.

Then we're going to load that file into a new variable called `$user` by using `Import-Csv` command with the file path `$filepath`.


### 3. Test PowerShell Script
Now we give the script a test to make sure we don't have any error by hitting the **"Play" button**. We're going to be prompted to enter the path to the CSV file, let's our path is `C:\Users\Administrator\Desktop\accounts.csv`. Here is the console:
```
PS C:\Users\Administrator> # Import required modules
Import-Module ActiveDirectory

# Prompt user for CSV file path
$filepath = Read-Host -Prompt "Please enter the path to your CSV file"

# Import the file into a variable
$users = Import-Csv $filepath
Please enter the path to your CSV file: C:\Users\Administrator\Desktop\accounts.csv     // enter the path

PS C:\Users\Administrator>
```
If we don't get any error, that means our CSV has been successfully read.


### 4. Loop Through Row of CSV File
We're going to loop through each row of the CSV file `accounts.csv` by using the `ForEach` command.

Once we import this CSV file, the first line will be considered a ***header***, next is going to loop through each of the following lines in the CSV file. Here is the `accounts.csv` open in a plain text editor:
```
First Name,Last Name,Job Title,Email Address,Organizational Unit
Mike,Terry,Office Manager,mike.terry@itflee.com,"OU=Office,OU=itFlee,DC=itflee,DC=com"
Ridley,Quin,Software Engineer,ridley.quin@itflee.com,"OU=Administrators,OU=itFlee,DC=itflee,DC=com"
Ridley,Dalton,Network Administrator,ridley.dalton@itflee.com,"OU=Administrators,OU=itFlee,DC=itflee,DC=com"
Rollo,Braith,Technical Analyst,rollo.braith@itflee.com,"OU=Office,OU=itFlee,DC=itflee,DC=com"
Stan,Kenzie,Support Specialist,stan.kenzie@itflee.com,"OU=Administrators,OU=itFlee,DC=itflee,DC=com"
Clyde,Braiden,Data Analyst,clyde.braiden@itflee.com,"OU=Office,OU=itFlee,DC=itflee,DC=com"
Jolyon,Clifton,Web Developer II,jolyon.clifton@itflee.com,"OU=Office,OU=itFlee,DC=itflee,DC=com"
Kelsey,Mason,Executive Assistant,kelsey.mason@itflee.com,"OU=Office,OU=itFlee,DC=itflee,DC=com"
Conway,Basil,System Administrator I,conway.basil@itflee.com,"OU=Administrators,OU=itFlee,DC=itflee,DC=com"
Earnest,Britton,Support Specialist,earnest.britton@itflee.com,"OU=Administrators,OU=itFlee,DC=itflee,DC=com"
```
Each one of these lines is going to be considered a `$user`.

Let's continue in the ***PowerShell*** script editor. We put all the information of each row into a variable `$user`. Then we're going to start by grabbing the value `'First Name'` attribute of `$user` and put it (`$user.'First Name'`) into a variable called `$fname`, which is short for first name. If we echo this `$fname` out, we're going to see the first name of every user starting from `Mike` and ending with `Earnest`:
```
# Import required modules
Import-Module ActiveDirectory

# Prompt user for CSV file path
$filepath = Read-Host -Prompt "Please enter the path to your CSV file"

# Import the file into a variable
$users = Import-Csv $filepath

# Loop through each row and gather information
ForEach($user in $users) {

    # Gather the user's information
    $fname = $user.'First Name'
    echo $fname
}
```

Let's give it a shot(by clicking **Play**). We can see it's started with `Mike` and ended with `Earnest`. So it's going through each line and outputting the first name:
```
PS C:\Users\Administrator> # Import required modules
Import-Module ActiveDirectory

# Prompt user for CSV file path
$filepath = Read-Host -Prompt "Please enter the path to your CSV file"

# Import the file into a variable
$users = Import-Csv $filepath

# Loop through each row and gather information
ForEach($user in $users) {

    # Gather the user's information
    $fname = $user.'First Name'
    echo $fname
}
Please enter the path to your CSV file: C:\Users\Administrator\Desktop\accounts.csv     // enter file path
Mike
Ridley
Ridley
Rollo
Stan
Clyde
Jolyon
Kelsey
Conway
Earnest

PS C:\Users\Administrator> 
```

We add a new user in Active Directory by using `New-ADUser` command, it doesn't matter what order you doing this stuff `-Name`, `-GivenName`...etc.
```
# Import required modules
Import-Module ActiveDirectory

# Prompt user for CSV file path
$filepath = Read-Host -Prompt "Please enter the path to your CSV file"

# Import the file into a variable
$users = Import-Csv $filepath

# Loop through each row and gather information
ForEach($user in $users) {

    # Gather the user's information
    $fname = $user.'First Name'
    $lname = $user.'Last Name'
    $jtitle = $user.'Job Title'
    $emailaddress = $user.'Email Address'
    $OUpath = $user.'Organizational Unit'

    # Create new AD user for each user in CSV file
    New-ADUser -Name "$fname $lname" -GivenName $fname -Surname $lname -UserPrincipalName "$fname.$lname" -EmailAddress $emailAddress -Path $OUpath -AccountPassword $securePassword -ChangePasswordAtLogon $true -Enabled $true
}
```
Note that you don't have wrap with **single quotes `'`** if your attribute didn't contain **`space`**.

Since the password and the ***secure string* `$securePassword`** is not created yet, let's create a static password and then convert it to ***secure string***.
```
# Import required modules
Import-Module ActiveDirectory

# Create a new password
$securePassword = ConvertTo-SecureString "ABC@1234" -AsPlainText -Force

# Prompt user for CSV file path
$filepath = Read-Host -Prompt "Please enter the path to your CSV file"

# Import the file into a variable
$users = Import-Csv $filepath

# Loop through each row and gather information
ForEach($user in $users) {

    # Gather the user's information
    $fname = $user.'First Name'
    $lname = $user.'Last Name'
    $jtitle = $user.'Job Title'
    $emailaddress = $user.'Email Address'
    $OUpath = $user.'Organizational Unit'

    # Create new AD user for each user in CSV file
    New-ADUser -Name "$fname $lname" -GivenName $fname -Surname $lname -UserPrincipalName "$fname.$lname" -EmailAddress $emailAddress -Path $OUpath -AccountPassword $securePassword -ChangePasswordAtLogon $true -Enabled $true
}
```

Let's give it a test by running it again. If we get no error, we should created a bunch of accounts:
```
PS C:\Users\Administrator> # Import required modules
Import-Module ActiveDirectory

# Create a new password
$securePassword = ConvertTo-SecureString "ABC@1234" -AsPlainText -Force

# Prompt user for CSV file path
$filepath = Read-Host -Prompt "Please enter the path to your CSV file"

# Import the file into a variable
$users = Import-Csv $filepath

# Loop through each row and gather information
ForEach($user in $users) {

    # Gather the user's information
    $fname = $user.'First Name'
    $lname = $user.'Last Name'
    $jtitle = $user.'Job Title'
    $emailaddress = $user.'Email Address'
    $OUpath = $user.'Organizational Unit'

    # Create new AD user for each user in CSV file
    New-ADUser -Name "$fname $lname" -GivenName $fname -Surname $lname -UserPrincipalName "$fname.$lname" -EmailAddress $emailAddress -Path $OUpath -AccountPassword $securePassword -ChangePasswordAtLogon $true -Enabled $true
}
Please enter the path to your CSV file: C:\Users\Administrator\Desktop\accounts.csv     // enter file path

PS C:\Users\Administrator>
```
Open the Active Directory Users and Computers MMC, on the left pane, click **"itflee.com"** -> **"itFlee"** -> **"Administrators"** and **"Office"**. If we hit `F5` on this **OU**, now we can see that the new accounts have been created.

Save as the script file and call it `CreateUsersFromCSV.ps1`. Back to the desktop, you now can run the script by right-clicking the `CreateUsersFromCSV` file icon, then click **"Run with PowerShell"**. By providing the file path, you can still create a bunch of user accounts in Active Directory.


- ### `New-ADUser` Options
Note that all the `New-ADUer` options are listed in the following website:

https://learn.microsoft.com/en-us/powershell/module/activedirectory/new-aduser?view=windowsserver2022-ps

