
<hr />  

### ![Reverse Super(Command) with Ctrl keys](https://askubuntu.com/a/766216)  
I just installed Ubuntu 16.04 dual boot on my MBP13" yesterday. For Ubuntu 16.04, here's how i did it:  

Step 1: Launch terminal  

Step 2: Edit X Keyboard Extension  

```bash
sudo vim /usr/share/X11/xkb/symbols/pc
```

Step 3: Make the following changes. Ensure your file looks like this:  

```bash
key <LCTL> {    [ Super_L       ]   };
key <LWIN> {    [ Control_L     ]   };

...

key <RCTL> {    [ Super_R       ]   };
key <RWIN> {    [ Control_R     ]   };
```

Step 4: Clear xkb's cache  
```bash
sudo rm -rf /var/lib/xkb/*
```
Step 5 (conditional): If the keys are not swapped after step 4, restart your computer. It worked for me after this.  

Hope it helps, good luck!  

<hr />  

### ![Disable automatic remote printer installation](https://askubuntu.com/a/556963)  



In `/etc/cups/cups-browsed.conf`, set directive:  

`BrowseProtocols none`  

Afterwards, run service cups-browsed restart and service cups restart. There should be no printers visible, except those you've added yourself.  

<hr />  

### ![Change Function Key behavior](https://help.ubuntu.com/community/AppleKeyboard#Ubuntu_9.04_to_12.04_LTS_.28Precise_Pangolin.29)  


This section of the document describe how to change the behavior of 'fn' key to better match what user expect. (See #201711, #162083)  

Here a description of each behavior :  

>0 = disabled : Disable the 'fn' key. Pressing 'fn'+'F8' will behave like you only press 'F8'  
1 = fkeyslast : Function keys are used as last key. Pressing 'F8' key will act as a special key. Pressing 'fn'+'F8' will behave like a F8.  
2 = fkeysfirst : Function keys are used as first key. Pressing 'F8' key will behave like a F8. Pressing 'fn'+'F8' will act as special key (play/pause).  

##### Ubuntu 9.04 to 12.04 LTS (Precise Pangolin)  

Temporarily  

The following command will change the behaviour of 'fn' key with immediate effect, but restarting will reset the configuration:  

`$ echo 2 | sudo tee /sys/module/hid_apple/parameters/fnmode`  

(The meaning of fnmode values is as described in the preceding section.)  

Permanently  

Methods described in this section will change the behavior permanently. There are several ways to proceed with this modification. Each sub-section describes one way to permanently change the configuration.  

With .conf file (Recommended)  

1. Run the following command to append the configuration line to the file __*/etc/modprobe.d/hid_apple.conf*__ creating it if necessary:  

`$ echo options hid_apple fnmode=2 | sudo tee -a /etc/modprobe.d/hid_apple.conf`  

2. Trigger copying the configuration into the initramfs bootfile.  

`$ sudo update-initramfs -u -k all`  

3. Optionally, reboot  

`$ sudo reboot`  

With sysfs.conf  

1. Edit the __*/etc/sysfs.conf*__ file, creating it if necessary.  

`sudo gedit /etc/sysfs.conf`  

2. Add this lines to the end of the file.  

`module/hid_apple/parameters/fnmode = 2`  

3. Reboot  

<hr />  

[30 Things to do After Installing Ubuntu 18.04 LTS (all-in-one video)](https://www.youtube.com/watch?v=BLVtxpm5c2A)  


###  Minimize the window through click the dock
`gsettings set org.gnome.shell.extensions.dash-to-dock click-action 'minimize'`
