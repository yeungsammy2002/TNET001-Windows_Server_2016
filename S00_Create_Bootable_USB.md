# Create Windows Server 2016 Bootable USB



- ## Download Window Server 2016 ISO
1. Download ***Windows Server 2016 ISO*** file (i.e. for ***Microsoft VLSC***)
2. Insert a USB Drive (***8GB*** above)



- ## Disk part - Command Prompt 
1. In Windows Start, search ***"cmd"*** -> right click ***"Command Prompt"*** -> ***"Run as administrator"***
2. In the windows system 32, run `diskpart`
   ```
   C:\WINODWS\system32\diskpart
   ```
3. In disk part, run `list disk`, you should see something like this:
   ```
   DISKPART> list disk
   Disk ###  Status         Size     Free     Dyn  Gpt
   --------  -------------  -------  -------  ---  ---
   Disk 0    Online          223 GB      0 B
   Disk 1    Online          931 GB  1024 KB   *    *
   Disk 2    Online           14 GB      0 B
   Disk 3    Online           14 GB      0 B        *
   ```
4. Run `select disk [number]`, i.e. `select disk 3`, you should see something like this:
   ```
   DISKPART> list disk
   Disk 3 is now the select disk
   ```
   If you run `lisk disk` again, you should see something like this:
   ```
     Disk ###  Status         Size     Free     Dyn  Gpt
     --------  -------------  -------  -------  ---  ---
     Disk 0    Online          223 GB      0 B
     Disk 1    Online          931 GB  1024 KB   *    *
     Disk 2    Online           14 GB      0 B
   * Disk 3    Online           14 GB      0 B        *
   ```
5. Before make the partition, run `clean`, it will literally remove all paritions. You should see something like this:
   ```
   DISKPART> clean
   DiskPart succeeded in cleaning the disk.
6. Run `convert MBR`, otherwise, it won't work with `active` command:
   ```
   DISKPART> convert MBR
   DiskPart successfully converted the selected disk to MBR format.
   ```
7. Run `create partition primary` to create ***primary partiton***, you should see something like this:
   ```
   DISKPART> create partition primary
   DiskPart succeeded in creating the specified partition.
   ```
8. If you run `list partition`, you should see something like this if the parition was successfully created:
   ```
    DISKPART> list partition

    Partition ###  Type              Size     Offset
    -------------  ----------------  -------  -------
    * Partition 1    Primary             14 GB  1024 KB
   ```
   You see the partition is already selected, if not, run `select partition 1`
9. Run `active` to make that an ***active partition***, you should see something like this:
   ```
   DISKPART> active
   DiskPart marked the current partition as active.
   ```
   Now you have a partition, but don't have a drive letter, and is not formatted.
10. Run `format fs=exfat quick label=[usb_name]`, `fs` for ***file system***, `exfat` is going to be requied for ***Windows Server 2016/2019*** and is too big for `win32`, `quick` will be tell to ***quick format***, you should see something like this:
   ```
   DISKPART> format fs=exfat quick label="winser16"
   100 percent completed
   DiskPart successfully formatted the volume.
   ```
11. Run `exit` to exit the disk part, you should see something like this:
   ```
   DISKPART> exit
   Leaving DiskPart...
   ```
**#Don't close the ***command prompt*** window**



- ## Copy ISO to USB on Command Prompt
1. Figure out the ***ISO Mounted drive letter***, i.e. `h:`, then change to `h:` by running `h:`
   ```
   C:\WINDOWS\system32>h:
   H:\>
   ```
2. Change directory to `boot` folder by running `cd boot`:
   ```
   H:\>cd boot
   H:\boot>
   ```
3. Run `bootsect /help` to check if `nt60` parameter is available 
4. Figure out the ***empty USB drive letter***, i.e. `g:`, then run `bootsect /nt60 g:`, you should see something like this:
   ```
   H:\boot>bootsect /nt60 g:
   Target volumes will be updated with BOOTMGR compatible bootcode.

   G: (\\?\Volume{3d6eb68b-b190-11ed-b357-7085c2d18457})

        Successfully updated exFAT filesystem bootcode.

   Bootcode was successfully updated on all targeted volumes.
   ```
5. Copy all the content to the ***empty USB drive*** by running `xcopy h:\*.* g:\ /E /H /F`, `h:*.*` is the **source location**, `g:\` is the **destination**, `/E` stands for ***empty directory***, `/H` stands for ***hidden directory*** and `/F` shows us **what the computer is doing**:
   ```
   H:\boot>xcopy h:\*.* g:\ /E /H /F
   H:\autorun.inf -> G:\autorun.inf
   H:\bootmgr -> G:\bootmgr
   H:\bootmgr.efi -> G:\bootmgr.efi
   H:\setup.exe -> G:\setup.exe
   H:\NanoServer\NanoServer.wim -> G:\NanoServer\NanoServer.wim
   ...
   ```

   