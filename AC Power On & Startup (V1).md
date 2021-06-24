*AmberCry Kit Power on and Startup Guide*

Network Information:
  The kit network is 10.1.x.x/16. Each individual kit has it's own subnet, kit 1 is 10.1.6.x, kit 2 is 10.1.7.x, and kit 3 is 10.1.8.x
  Analysts will operate on the 10.1.9.x network, and IT administration will operate on 10.1.5.x
  Each kit has remote management capabilities under the same IP Schema. You can remotely manage the Chassis and the individual blades. Chassis Management Console(CMC)'s IP is always 10.1.x.2, where x reflects the kit subnet as above. Blade 1's integrated Dell Remote Access Console(iDRAC) is always 10.1.x.3 and Blade 2's iDRAC is always 10.1.x.4
  ESXi will always be reachable via http://10.1.x.10
  Moloch will always be reachable via http://10.1.x.20:8005
  Moloch has an extra interface for capture. It's IP is 10.1.x.21
  Kibana will always be reachable via http://10.1.x.11:5601
  Unless explicitly specified, the login passwords will always be 'Br111ckSquad!!!'
  Remember the above information, as it will be referred to below.
 
Required Components:
  - Kit x Chassis
  - Kit x Blades 1 and 2
  - Three RJ45 tipped ethernet cable
  - One SFP 1G Ethernet adapter
  - One TPLink Unmanaged Switch
  - One Laptop
  - All assosciated power cables and surge protectors
  
Background Information:
  This next section is important to understand for context in the following steps. It is important to ensure that the kit blades go to the matching kit chassis, e.g. Kit 1 Blades to Kit 1 Chassis. You can tell using the serial numbers on the kit blades and chassis. For example the serials starting with 'ID9K' on both chassis and blades are the correct ones. The blades ending with '01' and '02' are kit 1 and go to the chassis ending in '01' as well. Kit 2 blades are '03' and '04' and go to the chassis ending in '02'. Kit 3 blades are '05' and '06' and go to the chassis ending in '03'. They will not network correctly if plugged in wrong. 
  When installing or "plugging in" any component of this kit, if it has to be forced, it's being plugged in incorrectly. It should slide in and seat well. If not, find someone with more experience to assist.
  On the chassis, there are arms in the blade slots that need to be slid out before installing the blades. They slide out much like dresser drawer rails. There is an upside-down 'L' shaped tab above each arm that needs to be pushed up to slide those arms out. 
  On the chassis, in the top row of input ports, more on the right side of center, there is an ethernet port that allows a user to plug in a laptop to access the CMC. You will need to plug in one ethernet cable here, furthermore referred to as the "Chassis Management Port"
  Below the Chassis Management Port, there are a total of twelve larger ports. These ports cannot be plugged into with just an RJ45 Tipped ethernet cable. They require an SFP to be plugged in first. Install the SFP with the serial number facing upwards, and then plug the ethernet cable into the SFP. 
  To explain the ports, ports labelled 1-4 are wired directly into the top blade. Ports labelled 5-8 are wired directly into the bottom blade. Ports labelled 9-12 are more complicated. They network the blades together and will provide data from both blades just by plugging into one of them
  Further explanation of the ports, ports labeled 2, 4, 6, 8, 10, and 12 are disabled. If you plug anything into them, you will not receive data or connectivity. Furthermore, Ports labelled 9 and 11 are both able to transmit data from all of the following ports: 1,3,5 and 7. So to network the kits as simply as possible, best practice is to install an SFP in port 9 to maintain connectivity to all blades and their active ports. 
  Before powering on the kit, ensure all cables are plugged in where they need to be. If nothing is plugged in when the kit is powered on, after 20 seconds pass, ALL PORTS WILL BE DISABLED, which requires a complete power down and power on cycle to reset. 
  The Chassis will be ready to power on when a blue light that looks like a heartbeat signal from an electrocardiogram comes on. This light will be directly to the right of the power button, which resides in the top left corner of the chassis
  Moloch Services will not run until Elastic Search services are up and running on each node. These nodes reside on ESXi(this is a hypervisor operating system) as Virtual Machines, 
  
Power On and Startup Steps:
    1. Begin by pulling the designating where you have enough space and convenience to set up the AmberCry Kit. There needs to be a nearby powersource to plug in a surge protector.
    2. Pull out the Chassis from the pelican case. Verify the serial number and place the chassis where you want to set it up.
    3. Pull out the first blade from the pelican case. Verify the serial number to ensure it is being installed in the correct chassis. If it is Blade 2, it will need to be installed in the bottom slot. If it is Blade 1, it will need to be installed in the top slot. On the front of the blade, there is a small protrusion that looks like a handle with a blue tab on it. Pull that blue tab and swing that handle out before installing the blades. Slide the blade into the slot gently until it will not go further, then close the handle to lock it in place. You should hear an audible 'click'.
    4. After installing the blades, place the unmanaged switch on top of the chassis and plug in ethernet cables into any port. It does not matter which ports because it is an unmanaged switch.
    5. Plug one ethernet cable into the analyst laptop. Plug one into The Chassis Managment Port.
    6. Install an SFP into port 11, and plug one ethernet cable into that SFP.
    7. Plug the power cables into the surge protector, the chassis, and the switch. The chassis will have the power ports on the right hand side of the chassis. Once power is connected, the fan blades will spin for a short period of time. This is normal.
    8. Once the blue 'heartbeat' light turns on next to the chassis power button, press the chassis power button. It will light up green if it is beginning to power on. The fans will spin again and stay on this time. This is normal.
    9. Wait a few moments, then log into the laptop with the password above. Open a Google Chrome Browser and type in the kit's CMC IP(specified above)
    10. Log into the CMC using the user of 'root' and password set above. When logged in, on the left side of the browser window you will see a section titled 'Server Overview'. You will see that there are four items beneath that, but only two are available, these would be 1 and 3. This is normal. The 1st selection goes to Blade 1 and the 3rd selection(or only other available option) goes to Blade 2. 
    11. Select the 1st server from the list to manage Blade 1. Near the top, you will see three tabs in the black bar. Select the one that says 'Power', then ensure the tab underneath it says 'Control'. When the power control options load, ensure 'Power On' radio button is selected, then click the blue "Apply" button near the bottom. You will be asked if you want to execute the server control action. Select yes. Repeat for Blade 2
    12. Navigate to the Blade 1 iDRAC IP(specified above). Log in with the user of 'root' and the password set above. 
    13. Scroll to the bottom of the page once logged in. On the right side of the web page will be a thumbnail underneath a title that says "Virtual Console". Click on the thumbnail.
    14. A new window will open that will show a boot process. This is going to be the Boot up process for ESXi. Do not press any options, let it boot to the preset defaults. You will know that the boot process is complete when you see a menu that says something to the effect of "Navigate to http://10.1.x.10 to manage this device"
    15. Navigate to the ESXi IP(specified above). Log in using the user of 'root' and password set above. 
    16. On the lefthand side of the webpage will be a short list. Click on the item that says "Virtual Machines". When they load, select the top checkbox above the list to select all the virtual machines(a check will auto populate in each box next to each virtual machine) and select the "Power On" option. 
    17. Wait for the VM's to power on. Once powered on, click on the VM titled "node1 -.11", then click the thumbnail to enter the virtual machine.
    18. Log in under the default user(should be named "gucci") with the password set above.
    19. Right-click on the desktop of the VM and select "open terminal". Type in the command "systemctl status elasticsearch" and verify that the output says "Active" and/or "Running"
    20. In the same terminal session, type in "systemctl status kibana" and verify the output says "Active" and/or "Running". If both are running, close out of the Virtual Machine and continue. If not, contact someone with an infrastructure JQR for help.
    21. Navigate the the Blade 2 iDRAC IP(specified above). Log in with the user of 'root' and the password set above.
    22. Scroll to the bottom of the page once logged in. On the right side of the web page will be a thumbnail underneath a title that says "Virtual Console". Click on the thumbnail.
    23. The boot process for Blade 2 should be complete by now. If not, wait for it to complete. When it is complete, there will be a login prompt for the user "gucci", or a blue screen with the time on it. Log in with the password set above. If the blue screen is what you see, click and drag upwards to get to the login prompt. If the screen is green and says "No Input", try to wake the server be clicking on the screen. If it doesn't work, contact someone with an Infrastructure JQR for help.
    24. Right click on the Blade 2 desktop after logging in, and select "open terminal"
    25. Verify the Elastic Cluster is up and running by running the command "sudo curl -XGET 'http://10.1.x.11:9200/cluster/health?pretty'". (there is an underscore before the "cluster" in the command) The output should have the word "green" next to the status. If not, contact someone with an infrastructure JQR for help.
    26. 
