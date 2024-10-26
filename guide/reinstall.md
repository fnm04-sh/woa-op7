<img align="right" src="https://github.com/fnm04-sh/woa-op7/blob/main/op7.png" width="450" alt="Windows 11 running on hotdog/guacamole">

# Running Windows on the OnePlus 7 Pro / 7T Pro

## Installing Windows

### Prerequisites
- [Renegade UEFI](https://github.com/edk2-porting/edk2-msm/releases/tag/2301.1)

- [Windows on ARM image](https://arkt-7.github.io/woawin/)
  
- [Drivers](https://github.com/fnm04-sh/woa-op7/releases/tag/Drivers)

- [UEFI image](https://github.com/fnm04-sh/woa-op7/releases/tag/UEFI)

### Boot Renegade UEFI
> Replace `path\to\renegade_uefi.img` with the actual path of the image
```cmd
fastboot boot path\to\renegade_uefi.img
```

### Entering mass storage mode
- In Renegade navigate by volume buttons to **UEFI Boot Menu** and select **USB Attached SCSI (UAS) Storage** and boot

### Installing Windows
> [!Warning]
> DO NOT USE 24H2!!!

> Replace `path\to\install.esd` with the actual path of install.esd (it may also be named install.wim or 22631.2861.XXXXXXX.esd)

```cmd
dism /apply-image /ImageFile:path\to\install.esd /index:6 /ApplyDir:X:\
```

> If you get `Error 87`, check the index of your image with `dism /get-imageinfo /ImageFile:path\to\install.esd`, then replace `index:6` with the actual index number of **Windows 11 Pro** in your image

### Copying your boot.img into Windows
- Drag and drop the **rooted_boot.img** from the **platform-tools** folder into the **WINONEPLUS** disk in Windows Explorer, then rename it to **boot.img**.

### Installing Drivers
- Download and unpack the driver archive for your device, then open the `OfflineUpdater.cmd` file (if an error shows up, run `OfflineUpdaterFix.cmd` instead)

> If it asks you to enter a letter, enter the drive letter of **WINONEPLUS** (which should be **W**), then press enter
  
#### Create Windows bootloader files
> If any error shows up, such as "Failure when attempting to copy boot files", open `diskpart` again and assign any new letter to **ESPONEPLUS**, then replace the letter `Y` in the next command with the letter that you just added.
```cmd
bcdboot X:\Windows /s Y: /f UEFI
```

### Reboot to fastboot
```cmd
adb reboot bootloader
```

#### Boot into the UEFI
> Download the UEFI image for your device, then replace `path\to\devicename-uefi.img` with the actual path of the UEFI image
```cmd
fastboot boot path\to\devicename-uefi.img
```

## Finished!
