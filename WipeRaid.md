## Wiping Raid Configuration
### Configuring BOSS-S1 RAID Controller

It is critical to reprovision the BOSS-S1 RAID controller before installing a new operating system to remove remnants of previously installed operating systems.

1. Boot the desired FC640
> To power on the FC640 follow FC640: Power On Procedures or KVM: Power On Procedures as appropriate
2. Press and depress the KVM selector button until the desired FC640 displays a flashing blue light next to the power button
> This indicated that the KVM is currently displaying the identified FC640 console
3. During the boot cycle, press F10 on the keyboard when prompted
> This action initiates entry into the Lifecycle controller for the identified FC640
4. Click “Hardware Configuration” from the left plane
5. Click “Configuration Wizards” link
6. Click “Raid Configuration” link
7. From the Raid Controller list, select “BOSS-S1”
8. Click Next
9. Select “Raid 1”
10. Click Next
11. Check the “Select All” checkbox under Disk menu
12. Click Next
13. Enter the following under Virtual Disk Name: VD_FRONT_R1
14. Click Next
15. Click Finish
16. Click Yes to confirm RAID configuration
17. Click OK to confirm RAID configuration changes
18. Click Exit in the upper right corner
19. Click Yes to confirm reboot
20. Repeat steps 1 through 19 for the FC640 installed in chassis bay 3

### Setting PERC H730 Raid Level and Assigning Disks
It is important to configure a virtual disk prior to installing operating systems on the FC640. 
The following steps will guide you through configuring the 8 internally connected 7.8 Terabyte drives into an appropriate Raid level for the operating system 
you will be installing.
1. Reboot or initiate a power on action for the FC640 installed in chassis bay 1
2. During the boot process, press “CTRL + R” when prompted to enter RAID configuration
3. At the PERC H730 BIOS Configuration Utility, press F2 to enter the controller action menu
4. Scroll down with arrows to “Convert to RAID capable”
5. Press Enter
6. Press Spacebar 8 times to select all disks
7. Press the tab button until OK is highlighted
8. Press Enter
9. Scroll down or up using arrow buttons to “No Configuration Present !”
10. Press F2 to enter action menu
11. Scroll down using arrow buttons to “Create New VD”
12. Press Enter
13. At the virtual disk configuration menu, press Enter to open RAID level selection menu
    - If installing ESXi, scroll using arrows down to RAID-50 and press Enter
    - If installing Security Onion, scroll using arrows to RAID-0 and press Enter
14. Tab to “Disks Per Span” textbox
15. If installing ESXi, enter 4
15. If installing Security Onion, no entry is required
16. Tab to Disk listing area
17. Press Spacebar 8 times to select all disks
18. Tab to “Virtual Disk Name” textbox
19. For ESXi installations, enter “VD_INTERNAL_R50”
19. For Security Onion installation, enter “VD_INTERNAL_R0”
20. Press tab button until “OK” is highlighted
21. Press Enter
22. Scroll using arrow keys to “VD_INTERNAL_R<RAID_LEVEL>”
23. Press F2 to enter action menu
24. Scroll down using arrows to “Initialization”
25. Use right arrow to open “Initialization” sub-menu
26. Scroll down using arrows to “Fast Init.”
27. Press Enter
28. Use arrow keys to highlight “Yes”
29. Press Enter
> This initialization will take approximately three seconds
30. Press Enter when the completion prompt appears
31. Press Escape to exit the RAID configuration utility
32. Press CTRL+ALT+DELETE to complete reboot action
> You have now configured the RAID level and assigned disks for the PERC H730 on the FC640 installed in chassis bay 1
33.Repeat steps 1 through 19 for the FC640 installed in chassis bay 3
34. Reboot

POST REBOOT CONTINUING CONFIGURATION
1. Press F10 to select Lifecycle Controller
2. Select Configure Raid
3. Select Dropdown and click PERC H730P
4. Select Raid level, then select Next
    -For ESXi, select Raid 50. 
    -For CentOS, select Raid 0
5. Click the checkbox to select all physical disks at the bottom. Leave the defaults, except span lenght. Select Next when done
    -For ESXi, select 4
    -For CentOS, no entry is required
6. Name the VD Disk as follows: "VD_INTERNAL_R<RAID LEVEL>", leave all other defaults, select next when done
    -example : "VD_INTERNAL_R50"
7. Select Finish, then click Yes when prompted to continue. 
8. Select Exit, then click Yes to reboot.
   
