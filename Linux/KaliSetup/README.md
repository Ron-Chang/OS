# Kali Installation  

Hardware: MacBook Pro 2015 Mid  
__Installed on External HDD with WinOS (Not BootCamp)__  

Basically, follow the [Official Instruction](https://docs.kali.org/installation/kali-linux-dual-boot-on-mac-hardware)  

## 0. Preparation

1. Prepare a USB drive(over than 4 GB)  
2. [Download Kali Linux](https://www.kali.org/downloads/)  
3. <font color="red">!! Backup any important information on the device !!</font>  

## 1. [Install rEFInd Boot Manager](https://www.rodsbooks.com/refind/installing.html)  
It's easy if we just follow the [installation Official](https://docs.kali.org/installation/kali-linux-dual-boot-on-mac-hardware) in this part.  

## 2. Then create a Bootable USB drive   
Go to [Gregory Conrad's website](https://www.gsconrad.com/), check `download` -> [`(New-With GUI) Boot Drive Maker for Mac`](https://github.com/GregoryConrad/BootableDriveMaker/releases/download/v7.0/Bootable.Drive.Maker.dmg)  
[Follow this tutorial](https://youtu.be/kRgKlcm1XPI?t=73), but in [1:54](https://youtu.be/kRgKlcm1XPI?t=114) select the `Kali ISO` which you downloaded instead of `Ubuntu ISO`.  

## 3. Boot into `Kali bootloader menu` through `rEFInd`.  
Select `Live(amd64)` or `Kali Live`.  

## 4. Use `GParted` to shrink the partition.  
Hit `command(super)` button and keying `GParted`.  
<font color="red">!! Make sure you select correct hard drive !!</font>  
Shrink two partition.  
- `Kali partition` with `ext4`  
- `swap partition` with `swap area`  

reboot to `Kali bootloader menu`.  

## 5. Installation Procedure  
Select `Graphical install` or `Start install`(It depends on the `Kali ISO` version you download)  

After you finish your language and keymap, here comes a tricky part.

Some people will see an error ["Can't install Kali Linux from USB, fails to find CD-ROM drive"](https://superuser.com/a/962993), I saw this error once at the first time I installed. It also showed me the issue with `unetbootin` (Don't worry about it, we make the bootable USB by `Boot Drive Maker` instead of `unetbootin`).  

If everything goes well, you probably just move on to the `detect network`.  

- Select Wifi.  
- Input WPA2 password.  
- Input Hostname.  
- Input password for the root account.  
- Set time zone.  

## 6. Select a `disk` and `partition`  

1. Select `Manual`.  
2. Select `Kali partition` you can check it with `label`, `name` or `format type` to figure out.  
3. make sure mount point is `"/"`, means root, and format type is ext4, select `done setting`.  
4. Select `swap partition`, format type is swap area.  
5. Select `Finish partitioning and write changes to disk`, then continue.  
6. `INSTALLING...`,wait until it shows further option.  
7. Use a network mirror? Select `Yes`.  
8. Install GRUB bootloader? Select `Yes`.  
9. Finally, click `Continue` to finish installing Kali Linux.  
__It is highly recommend that you restart your machine at this stage.__  

## 7. If your Kali install on the same disk with `MacOS` or `GPT WinOS`.  

#### - Convert the Master Boot Record (MBR) to GUID Partition Table (GPT)  
>[Troubleshooting](https://apple.stackexchange.com/questions/323461/triple-boot-macos-high-sierra-linux-mint-and-windows-with-refind)  
1. boot into `Kali Live` again.  
2. open `Terminal`.  
```bash
apt-get update
apt-get install gdisk
```
Check the disk name by `GParted`(See Step 4)
In my case, I installed Kali on `sdc`

```bash
gdisk /dev/sda
```
You will see this,  
```bash
GPT fdisk (gdisk) version 0.8.5

Partition table scan:
MBR: protective
BSD: not present
APM: not present
GPT: present

Found valid GPT with protective MBR; using GPT.
```
[Check how to backup GPT header](https://www.rodsbooks.com/gdisk/repairing.html)

follow the order and input `p`,`x`,`n`,`w`,`Y` with `Return` between all of them.

reboot.

After the steps above, `WinOS` should booting.

#### - Convert the Master Boot Record (MBR) to hybrid (MacOS)  
Follow [Kali Linux Installation Procedure](https://docs.kali.org/installation/kali-linux-dual-boot-on-mac-hardware), from Step 12 and 13.  
