# ZmaCorK
Z390-A PRO + macOS + OpenCore + i5-9600K = ZmaCorK
 
# My macOS 11.x OpenCore Hackintosh
 
## The Following Equipment is Required
 `MSI Z390-A PRO`

 `Intel i5-9600K`
 
## Pre-Install Steps
### Resize The EFI/System Partition to 1GB
- I use **[MiniTool Partition Wizard](https://www.partitionwizard.com/free-partition-manager.html)** because it's simple and free.

*Note: The **MSR** Partition is `16MB`. It sits between our EFI and Windows Partitions. We cannot move unallocated space two partitions over.*

- Delete the **MSR** Partition
- Shrink the **Windows** Partition by `808MB`
- Extend the **EFI** Partition to `1GB`

*Note: 200MB original EFI size + 16MB MSR + 808MB from Windows = 1024MB*
- Apply and Reboot
 
### Download macOS Recovery Files
- Follow along **[here](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/winblows-install.html#downloading-macos)** until you reach **Making The Installer**.
- Once the downloads are finished create a folder named `com.apple.recovery.boot` and move `BaseSystem.chunklist` & `BaseSystem.dmg` into it.
- Drag the `com.apple.recovery.boot` folder to your `C:` drive.
 
### Download Repo
- Download my repo from GitHub or click **[here](https://github.com/ZeroOneZero/ZmaCorK/archive/refs/heads/main.zip)**
- Open the zip and extract just the `EFI` folder to your `C:` drive.

### Generate Unique Serials
- Download the config.plist editor from **[here](https://github.com/corpnewt/ProperTree)**
- Extract the zip and run the .bat file.
- In ProperTree, **Open->`C:\EFI\OC\config.plist`**
- Follow the **PlatformInfo** steps **[here](https://dortania.github.io/OpenCore-Install-Guide/config.plist/coffee-lake.html#platforminfo)** to generate your own unique Board Serial, MLB & UUID.
 - Find the **MAC Address** of your Ethernet card using this command: `ipconfig /all`
 - Enter the **MAC** without special charcters into the **Apple ROM** field.
 
*Note: You must complete those last 3 steps. I blanked out the corresponding 4 fields in the config.plist*

- Save the file and quit ProperTree

### Copy Files to EFI
- Run a **Command Prompt** as **Administrator** and copy and paste these commmands:

`mountvol X: /S`

`xcopy C:\EFI X:\EFI /E /H /C /I /Y`


`xcopy C:\com.apple.recovery.boot X:\com.apple.recovery.boot /E /H /C /I /Y`

*Note: This will mount the System Partition and copy the folders we moved to `C:` into it.*
 
### Add Boot Entry for OpenCore
- Download **[BOOTICEx64](https://m.majorgeeks.com/index.php?ct=files&action=download&)**
- Extract and run the portable .exe
- In BootICE, **UEFI->Edit Boot Entries**
- You will see **Windows Boot Manager** and possibly others in the list.
- Select **Add**, then paste `X:\EFI\BOOT\BOOTx64.efi` into the **File Name** box
- Click **Okay** and you should see **Successfully added boot entry**.
- Name this Boot Entry in the **Menu Title** field `OpenCore`
- Click on **Save current boot entry**
- Last, **Close->Exit** and reboot to enter the BIOS settings below.
 
## Setting Up The BIOS
 
### MSI Z390-A PRO / BIOS Revision: 7B98v1D

*Note: During boot repeatedly taping the **Delete** key on the keyboard will open the BIOS*
 
- `Factory Default Settings by Pressing F6`
- `Enter Advanced Mode by Pressing F7`
- `[Settings -> Advanced]: Above 4G memory/Crypto Currency mining: [Disabled]->[Enabled]`
- `[Settings -> Integrated Graphics Configuration]: Initiate Graphic Adapter: [PEG]->[IGD]`
- `[Settings -> Integrated Graphics Configuration]: Integrated Graphics Share Memory [64M]`
- `[Settings -> Super IO Configuration]: Serial(COM) Port: [Enabled]->[Disabled]`
- `[Settings -> Super IO Configuration]: Parallel(LPT) Port: [Enabled]->[Disabled]`
- `[Settings -> Windows OS Configuration]: Windows 10 WHQL Support: [CSM]->[UEFI]`
- `[Settings -> Windows OS Configuration]: Fast Boot: [Disabled]`
- `[OC -> CPU Features]: Intel VT-D Tech: [Disabled]`
- `[OC -> CPU Features]: CFG Lock: [Enabled]->[Disabled]`
- `[OC -> CPU Features]: SW Guard Extensions (SGX): [Software Controlled]->[Disabled]`
 
## Boot It Up
- After saving the BIOS changes, have your Display Port (DP) cable connected.
- I use a DP->HDMI cable that plugs into a ARC port on the TV so it pulls in the audio as well.
- Boot your PC pressing F11 until you see the Boot options screen
- Select OpenCore

*Note: May be listed as **UEFI OS***

- Select recovery.dmg to start macOS install.
- Refer **[here](https://dortania.github.io/OpenCore-Install-Guide/installation/installation-process.html#booting-the-opencore-usb)** for any troubleshooting.
