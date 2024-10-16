<img align="right" src="https://github.com/fnm04-sh/woa-op7/blob/main/op7.png" width="450" alt="Windows 11 running on hotdog/guacamole">

# Running Windows on the OnePlus 7 Pro / 7T Pro

## Partitioning your device

### Prerequisites
- Unlocked bootloader

- [ADB & Fastboot](https://developer.android.com/studio/releases/platform-tools)
  
- Any TWRP For Guacamole and Hotdog

- [Parted](https://github.com/fnm04-sh/woa-op7/releases/tag/parted)

### Notes
> [!WARNING]  
> 
> DO NOT REBOOT YOUR PHONE! If you think you made a mistake, ask for help in the [Telegram chat](https://t.me/woahelperchat).
> 
> Do not run all commands at once, execute them in order!
>
> YOU CAN BREAK YOUR DEVICE WITH THE COMMANDS BELOW IF YOU DO THEM WRONG!!!

### Opening CMD as an admin
> Download **platform-tools** and extract the folder somewhere, then open CMD as an **administrator**.
>
> It is recommended to keep this window open and use it throughout the entire guide.
> 
> Replace `path\to\platform-tools` with the actual path to the platform-tools folder, for example **C:\platform-tools**.
```cmd
cd path\to\platform-tools
```

#### Boot TWRP recovery
> [!Note]
> This image may not boot on OOS12, if this is the case, downgrade to OOS11 first, install Windows, then update back to OOS12.

> Open a CMD window inside the platform-tools folder, then (while your phone is in fastboot mode) run
```cmd
fastboot boot path\to\twrp.img
```

#### Backing up your boot image
> This will back up your boot image in the current directory
```cmd
adb pull /dev/block/by-name/boot boot.img
```
#### Unmount data
> Go to "Mount' and click to 'Data'

#### Push Parted to /sbin
```cmd
adb push parted /sbin
```
#### Get to adb shell
```cmd
adb shell
```
#### Enter to Partition table
> Change root acess to this folder
```cmd
chmod 755 /sbin/parted
```
#### Navigate to /sbin
```cmd
cd /sbin
```

### Partitioning guide
> Pick the one that applies to you

<details>
<summary><a><strong>For 128GB devices</strong></a></summary>

#### Preparing for partitioning
```cmd
./parted /dev/block/sda
```

#### Printing the current partition table
> Parted will print the list of partitions, userdata should be the last partition in the list.
```cmd
print
```

#### Resizing userdata
> Replace **$** with the number of the **userdata** partition, which should be **19** or **22**
```cmd
resizepart $
```
#### Write **48GB**
> Just write **48GB**
```cmd
End? [124GB]? 48GB
```
#### Creating ESP partition
> Replace **48GB** with the end value of **userdata**
>
> Replace **48.5GB** with the value you used before, adding **0.5GB** to it
```cmd
mkpart esp fat32 48GB 48.5GB
```

#### Creating Windows partition
> Replace **48.5GB** with the end value of **esp**
```cmd
mkpart win ntfs 48.5GB 124GB
```

#### Making ESP bootable
> Use `print` to see all partitions. Replace "$" with your ESP partition number, which should be **20** or **23**
```cmd
set $ esp on
```

#### Exit parted
```cmd
quit
```

  </summary>
</details>

<details>
<summary><a><strong>For 256GB devices</strong></a></summary>

#### Preparing for partitioning
```cmd
./parted /dev/block/sda
```

#### Printing the current partition table
> Parted will print the list of partitions, userdata should be the last partition in the list.
```cmd
print
```

#### Resezing userdata
> Replace **$** with the number of the **userdata** partition, which should be **19** or **22**
```cmd
resizepart $
```
#### Write **128GB**
> Just write **128GB**
```cmd
End? [252GB]? 128GB
```

#### Creating ESP partition
> Replace **128GB** with the end value of **userdata**
>
> Replace **128.3GB** with the value you used before, adding **0.3GB** to it
```cmd
mkpart esp fat32 128GB 128.3GB
```

#### Creating Windows partition
> Replace **128.3GB** with the end value of **esp**
```cmd
mkpart win ntfs 128.3GB 252GB
```

#### Making ESP bootable
> Use `print` to see all partitions. Replace "$" with your ESP partition number, which should be **20** or **23**
```cmd
set $ esp on
```

#### Exit parted
```cmd
quit
```

  </summary>
</details>


### Formatting data
- Format all data in TWRP, or Android will not boot.
- ( Go to Wipe > Format data > type yes )

#### Check if Android still starts
- Just restart the phone, and see if Android still works

## [Next step: Installing Windows](/guide/2-install.md)
