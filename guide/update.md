<img align="right" src="https://github.com/fnm04-sh/woa-op7/blob/main/op7.png" width="450" alt="Windows 11 running on hotdog/guacamole">

# Running Windows on the OnePlus 7 Pro / 7T Pro

### Prerequisites
- [Renegade UEFI](https://github.com/edk2-porting/edk2-msm/releases/tag/2301.1)
  
- [Drivers](https://github.com/fnm04-sh/woa-op7/releases/tag/Drivers)

### Boot Renegade UEFI
> Replace `path\to\renegade_uefi.img` with the actual path of the image
```cmd
fastboot boot path\to\renegade_uefi.img
```

### Entering mass storage mode
- In Renegade navigate by volume buttons to **UEFI Boot Menu** and select **USB Attached SCSI (UAS) Storage** and boot

### Update Drivers
> [!Note]
> This process will take +- 20 minutes. Do not worry, this is normal.

- Unpack the driver archive, then open the `OfflineUpdater.cmd` file (if an error shows up, run `OfflineUpdaterFix.cmd` instead)

> If it asks you to enter a letter, enter the drive letter of **WINONEPLUS** (which should be **W**), then press enter

#### Reboot your device
> Make sure to also change the UEFI image in Android, otherwise you may face a "blue screen of death" (BSoD) when booting Windows later.

## Finished!
