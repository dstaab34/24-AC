BOOTING AN OPERATING SYSTEM
1. Power Cycle the server
2. During boot, press F11 to enter BOOT MANAGER
3. Plug in bootable USB drive to server 
  - For ESXi use FD-10
  - For CentOS use FD-06
4. Select One-Shot UEFI BOOT Menu
5. Select Generic USB Boot

FOR ESXi
1. Hit enter to begin BOOT, or wait and let default BOOT occur.
2. When prompted, hit ENTER to continue
3. Press F11 to accept and continue
4. Highlight the DELL PERC H730P Device and hit ENTER to continue
5. Ensure US Default is selected and hit ENTER to continue
6. set password, hit ENTER to continue
7. Press F11 to Continue to install
8. Remove the USB Drive, then hit ENTER to Reboot after Install
9. After Reboot, oress F2, enter password set previously
10. Use arrow keys to select "Configure Management Network"
11. Use arrow keys to select IPv4 Configuration
12. Use arrow keys to select "Set Static IPv4 address and netwrok configuration" (use spacebar to select option)
13. Use arrow keys to scroll to IPv4 and Subnet mask(leave default gateway alone), configure as follows:
   - IPv4: 10.1.X.10
   - Subnet Mask: 255.255.0.0
14. Hit esc, then hit Y   


FOR CENTOS
1. Select "Test this Media and install CentOS 7"
2. Select "English" and continue
3. For Installation Destination, select "DELL PERC H730P" and leave "Automatically configure Partitioning" selected.
4. For Software selection, select "Server with GUI" and leave defaults.
5. For Network & Hostname:
  - set hostname to "gucci.molochX"
  - configure em1, in general tab, select always connect when evailable. in Ipv4, set method to manual, configure IP address as follows:
    + IPv4: 10.1.X.20
    + Netmask: 255.255.0.0
    + Default Gateway: 10.1.X.1
  - configure em3, in general tab, select always connect when evailable. in Ipv4, set method to manual, configure IP address as follows:
    + IPv4: 10.1.X.21
    + Netmask: 255.255.0.0
    + Default Gateway: 10.1.X.1
7. Select Done, then Begin Installation. During installation, set root password, and set user with username of "gucci" and same password as root password. Make gucci administrator.
8. Remove USB, then reboot
