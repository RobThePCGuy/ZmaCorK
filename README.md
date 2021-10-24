# ZmaCorK
Z390-A PRO / macOS / OpenCore / i5-9600K = ZmaCorK

# My macOS 11.x OpenCore Hackintosh

## This Equipment is Required

- **MSI Z390-A PRO**
- **Intel i5-9600K**
 
## Downloading The Recovery Image for macOS Big Sur
- Resize your EFI partition to 1 GB
- Follow along in this [guide](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/winblows-install.html#making-the-installer) until the part about putting the recovery files on a thumb drive. 
- Instead you will put them alongside the EFI folder once you do mountvol in the next few steps.

## Installing The EFI Files

1: Download this repo from github or click **[here](https://github.com/ZeroOneZero/ZmaCorK/archive/refs/heads/main.zip)**.

2: Open the zip and extract just the **EFI** folder to your **C:** drive.

3: Open an Admin Command Prompt and run:

```
cmd /c if not exist X: (mountvol X: /S) & xcopy C:\EFI X:\EFI /E /H /C /I

move X:\EFI\Microsoft\Boot\bootmgfw.efi X:\EFI\Microsoft\Boot\bootmgfw.efi.bak && copy X:\EFI\BOOT\BOOTx64.efi X:\EFI\Microsoft\Boot\bootmgfw.efi
```
**Do not do the 2nd above command if you need Secure Boot in order to boot Windows, i.e. Windows 11.*

## Setting Up The BIOS

### MSI Z390-A PRO / BIOS Revision: 7B98v1D
	Factory Default Settings by Pressing F6
	Enter Advanced Mode by Pressing F7
	[Settings -> Advanced]: Above 4G memory/Crypto Currency mining: [Disabled]->[Enabled]
	[Settings -> Integrated Graphics Configuration]: Initiate Graphic Adapter: [PEG]->[IGD]
	[Settings -> Integrated Graphics Configuration]: Integrated Graphics Share Memory [64M]
	[Settings -> Super IO Configuration]: Serial(COM) Port: [Enabled]->[Disabled]
	[Settings -> Super IO Configuration]: Parallel(LPT) Port: [Enabled]->[Disabled]
	[Settings -> Windows OS Configuration]: Windows 10 WHQL Support: [CSM]->[UEFI]
	[Settings -> Windows OS Configuration]: Fast Boot: [Disabled]
	[OC -> CPU Features]: Intel VT-D Tech: [Disabled]
	[OC -> CPU Features]: CFG Lock: [Enabled]->[Disabled]
	[OC -> CPU Features]: SW Guard Extensions (SGX): [Software Controlled]->[Disabled]

## Boot It Up
- After saving the BIOS changes make sure to have your Display Port (DP) cable connected.
- I use a DP->HDMI cable that plugs into a ARC port on the TV so it pulls in the audio as well.
- Once you start the PC it should take you to the OpenCore Bootloader.
- Select the recovery dmg to start macOS install.
- Refer [here](https://dortania.github.io/OpenCore-Install-Guide/installation/installation-process.html#booting-the-opencore-usb) for any troubleshooting.
