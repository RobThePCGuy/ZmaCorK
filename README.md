# ZmaCorK
Z390-A PRO + macOS + OpenCore + i5-9600K = ZmaCorK

# My macOS 11.x OpenCore Hackintosh

## The Following Equipment is Required

- `MSI Z390-A PRO`
- `Intel i5-9600K`
 
## Pre-Install Steps
### Resize The EFI/System Partition to 1GB
- For this I use **[MiniTool Partition Wizard](https://www.partitionwizard.com/free-partition-manager.html)**.
- Shrink the OS Part by `884MB`
- Delete the **MSR** Partition.
- Extend the EFI Partition to `1GB` 
- Apply and reboot.

### Download macOS Recovery Files
- Follow along in this [guide](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/winblows-install.html#downloading-macos) until you reach **Making The Installer**.
- Once you have the `BaseSystem.chunklist` & `BaseSystem.dmg` files create a folder called `com.apple.recovery.boot` and move them into it.
- Drag the new folder to your `C:` drive.

### Installing The EFI Files
- Download my repo from GitHub or click **[here](https://github.com/ZeroOneZero/ZmaCorK/archive/refs/heads/main.zip)**.
- Open the zip and extract just the `EFI` folder to your `C:` drive.
- Open an Admin Command Prompt and run:

- `mountvol X: /S`
- `xcopy C:\EFI X:\EFI /E /H /C /I`
- `xcopy C:\com.apple.recovery.boot X:\com.apple.recovery.boot /E /H /C /I`

*This command mounts the EFI Partition to X: then copies the EFI and recovery folders you moved to C: to the EFI Partition*

### Add Boot Entry for OpenCore
- Download **[BOOTICEx64](https://m.majorgeeks.com/index.php?ct=files&action=download&)**
- Extract and run the exe
- UEFI->Edit Eoot Entries
- At the least you'll see **Windows Boot Manager** in the list.
- Selct **Add** then type into the **File Name** box at the bottom of the window that opened.
`X:\EFI\BOOT\BOOTx64.efi`
- Click **Okay** and you should see **Sucessfully added boot entry**.
- In **Menu Title** type `OpenCore`.
- Click the box for **Boot this entry next time**.
- Click on **Save current boot entry**
- Lastly, close, exit and reboot to enter the BIOS settings below.

## Setting Up The BIOS

### MSI Z390-A PRO / BIOS Revision: 7B98v1D
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
- After saving the BIOS changes make sure to have your Display Port (DP) cable connected.
- I use a DP->HDMI cable that plugs into a ARC port on the TV so it pulls in the audio as well.
- Boot your PC pressing F11 until you see the Boot options screen 
- Selet OpenCore
- Select recovery.dmg to start macOS install.
- Refer [here](https://dortania.github.io/OpenCore-Install-Guide/installation/installation-process.html#booting-the-opencore-usb) for any troubleshooting.
