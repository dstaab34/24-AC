1. Navigate to the IP set up for ESXi from a browser, then log in with previously set credentials. 
2. First we need to configure datastroes, so select storage, then rightclick on datastore1 and rename it to "VIRTUAL_MACHINE_DATASTORE" and save
3. Click on "Devices" 
4. Select the first "Local NVME Disk" and then click "New Datastore" at the top
5. Type in "TOOLS_DATASTORE" then click next.
6. Ensure "Use full disk" is selected in partitioning options. 
7. Click next, then click finish
8. When asked, click yes
9. Then, select the next "Local NVME Disk" and click "Increase Capacity". 
10. Select "TOOLS_DATASTORE" when prompted, then click next
11. Select the "Local NVME Disk" from the device list then click next
12. Ensure "Use full disk" is selected in partitioning options.
13. Click next, then click finish
14. When asked, click yes
15. Click on "Local ATA Disk", then click "New Datastore"
16. Name the datastore "OS_DATASTORE"
17. Ensure "Use full disk" is selected in partitioning options. 
18. Click next, then click finish
19. When asked, click yes

NEXT, we will upload ISO files to the TOOLS_DATASTORE
1. Navigate back to the Datastores tab and click on TOOLS_DATASTORE
2. Click "DATastore Browser" at the top of the window
3. Click "Create Directory" and name the directory "ISO"
4. Select the ISO folder, then select "Upload"
5. Upload CentOS 7 (DVD) and pfSense images from C:\Users\Exotic\Desktop\Images, when finished, hit the "close" button.

NEXT, we will create portgroups
1. Navigate to the Networking tab on the lefthand side of the window. 
2. Click Port groups, then click "Add port group"
3. In the name, name it "PF to SBO" then click "Add"
4. Repeat for a port group named "PF to Customer"

Next, we will create the pfSense VM, boot, and configure it. 
1. Select the Virtual Machines tab on the lefthand side of the window.
2. Click "Create/Register VM"
3. Select "Create a new virtual machine", then click next
4. Enter in the name "pfSense- .1", leave the compatibility tab default.
5. Select Guest OS Family as "Other"
6. Select Guest OS Version as "FreeBSD 11 (64-bit)", then click next
7. Select "VIRTUAL_MACHINE_DATASTORE". DO NOT SELECT ANY OTHER DATASTORE TO STORE ANY VIRTUAL MACHINE ON
8. Select next, then under customize settings in the "Virtual Hardware" Tab, click "Add network adapter" twice.
9. Ensure the configuration matches the following(if not specified, leave the defaults):
  - CPU: 4
  - Memory: 16GB
  - Hard disk 1: 250GB
  - Click the arrow next to "Hard disk 1" and make sure "Thin Provisioning" is checked. THIS IS CRUCIAL
  - Network Adapter 1: VM Network
  - Network Adapter 2: PF to Customer
  - Network Adapter 3: PF to SBO
  - When you get to CD/DVD Drive one, select "Datastore ISO File", then navigate to TOOLS_DATASTORE > ISO and click on the pfSense image.
10. Click next, verify your presets, then click finish.
11. Click on the pfSense VM, then click the play button to open up a window of the pfSense Virtual Machine

NEXT We will follow BOOT Procedures for the pfSense, then configure it.
1. After power on, hit Enter to accept the Copyright and Distribution notice
2. Use arrow keys to select "Install pfSense", then hit Enter
3. Hit Enter to continue with default keymap
4. Ensure "Auto(UFS)" is selected and hit Enter
5. When installation finishes, highlight "No" and hit Enter
6. Select "Reboot" and hit Enter
7. After reboot, when prompted if VLANS should be set up, type "n" and hit Enter
8. Type in "vmx0" for the WAN interface and hit Enter
9. Type in "vmx1" for the LAN interface and hit Enter
10. when prompted for the Optional interface, don't type anything, just hit Enter
11. Type "y" when asked if you want to proceed, then hit Enter
12. When configuration finishes, type "2" then hit Enter to Set Interfaces IP Addresses
13. Type "1" to select the WAN interface, then hit Enter
14. Type "n" to deny configuration via DHCP then hit Enter
15. Don't type anything for the WAN address, then hit Enter
16. Repeate steps 14 and 15 for IPv6
17. type "y" to revert to HTTP as webconfigurator protocol
18. Press enter to continue, then press 2 again to configure interfaces IP addresses
19. press 2 to select LAN interface
20. enter 10.1.x.1/16
21. Don't type anything for an upstream IPv4 gateway
22. Don't type anything for LAN IPv6 address
23. Type "n" when prompted to enable DHCP server on LAN
24. take note of the address displayed to use webConfigurator. it should be "http://10.1.x.1/" as you set it
25. Press enter, type "11" to restart the web configurator, then close out of the VM without powering it off
26. Navigate to the web address in step 24. Sign in with default credentials (user: admin password : pfsense)
27. On the pfSense setup wizard, click next
28. click next again
29. leave hostname default, name the domain "kitX" where X is the kit number you are working on (e.g. "kit1"). Leave all other options default, click next
30. click next
31. On this page, deselect the checkbox next to "Block RFC1918 Private Networks" and "Block bogon networks". Leave all other options default
32. click next
33. Ensure your Lan configuration has the IP address of "10.1.x.1" and the subnet mask is 16, click next
34. type in a new admin password, remember this password
35. click next
36. click reload
37. click Finish
38. you have successfully completed setup configuration for pfSense
