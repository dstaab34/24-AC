# ESXI

Due to the prevalence of virtual machine usage in this build, a virtual machine hosting operating system is necessary.
Of all of the virtual machine hosting solutions avaialble, ESXi from VMWare is by far the easiest to use and configure.
ESXi is also free to use for 90 days at a time but this can be extended through simple command line commands.
ESXi installs directly to hard disk or RAID array and stores the virtual machines in virtual machine file system (vmfs) datastores.
In addition to hosting virtual machines, ESXi also controls the networking between the virtual machines, to include virtual switching and routing and interface assignment.
Installation, configuration and updating ESXi to properly function as a Master Node will be covered in this section.

---

## Installation
*Software Required: Rufus*

Standardized installation of the virtual machine host will enable repeatable deployment with the Amber Cry system.  
A standardized installation will also lead to more predictable performance and operator familiarity. 
For this section you will need an external VGA capable monitor, a USB Keyboard, and a bootable USB drive imaged with ESXI installation media.

1. Power on the chassis
> For steps to power on the chassis, reference the KVM: Power On Procedures section of this guide
2. Insert the VGA cable into the monitor and VGA port on the KVM
3. Insert the USB keyboard into the KVM USB port
4. Change the KVM display to the FC640 installed in Chassis Bay 1
> For instruction on changing and identifying KVM display settings, reference KVM: Configuration: Switching Between Console Views section of this guide
5. Insert the bootable USB drive prepared with ESXi into the usb port on the FC640 in Chassis Bay 1
   The USB port on the FC640 Compute/Storage blade is located in a recess behind the locking lever
6. Power on the FC640 installed in Chassis Bay 1
> To properly power on the FC640, reference FC640: Power On Procedures
7. During the boot process, Press F11 to enter the boot menu
8. Using arrow keys scroll down to One-Shot Boot Menu and press enter
9. Using arrow keys scroll down to Front USB option and press enter
10. When prompted press enter to boot from ESXI
11. At End User License Agreement (EULA) screen, press F11 to accept
12. Using arrow keys scroll down to ATA DELLBOSS and press enter
13. At keyboard layout selection, press enter to continue with US layout
14. Enter a root password 
15. Enter root password again in verify password textbox and press enter
16. at confirmation screen, press F11 to continue with installation
17. At installation completion screen, press enter to reboot
18. Remove bootable USB drive from FC640 usb port
