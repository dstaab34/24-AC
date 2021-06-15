STARTING FROM ESXi TO CREATE A VM FOR EACH ELASTIC NODE. REPEAT THE STEPS FOUR MORE TIMES TO CREATE YOUR CLUSTER
1. On the Virtual Machines tab, click "Create/Register VM"
2. Select "Create a new virtual machine", then click next
3. Enter in the name "nodex- .1x" where 'x' is the node number, leave the compatibility tab default. (e.g. node1- .11)
4. Select Guest OS Family as "Linux"
5. Select Guest OS Version as "CentOS 7 (64-bit)", then click next
6. Select "VIRTUAL_MACHINE_DATASTORE". DO NOT SELECT ANY OTHER DATASTORE TO STORE ANY VIRTUAL MACHINE ON
7. Select next, then under customize settings in the "Virtual Hardware" Tab, click "Add network adapter" twice.
8. Ensure the configuration matches the following(if not specified, leave the defaults):
  - CPU: 12
  - Memory: 64GB
  - Hard disk 1: 4TB
  - Click the arrow next to "Hard disk 1" and make sure "Thin Provisioning" is checked. THIS IS CRUCIAL
  - Network Adapter 1: VM Network
  - When you get to CD/DVD Drive one, select "Datastore ISO File", then navigate to TOOLS_DATASTORE > ISO and click on the CentOS 7 DVD image.
9. Click next, verify your presets, then click finish.
10. Click on the Elastic VM, then click the play button to open up a window of the Elastic Virtual Machine

NEXT, We will boot it and configure it.
1. Select "Test this media & Install CentOS 7) and hit enter
2. At the Installation Menu, select English (United States) and click continue
3. At software selection, select "Server with GUI"
4. At installation destination, ensure "VMWare Virtual disk" is selected, as well as "Automatically configure partitioning"
5. At network and Hostname, change hostname to "nodex.kitX" where 'x' is node number and 'X' is kit number (e.g. node2.kit3). then click apply.
6. still in network and hostname, select ens192 and click configure
7. Under the General tab, check "Automatically connect to this network when it is available"
8. Under IPv4 settings, change method to manual, and assign the address as follows:
  - Address: 10.1.X.1x where 'X' is the kit subnet and 'x' is the node number (e.g. 10.1.6.11)
  - Netmask: 255.255.0.0
  - Gateway: 10.1.X.1 where 'X' is the kit subnet (e.g. 10.1.6.1)
9. Click save, ensure ens192 is connected and on, then click done.
10. Click begin installation. set root password and create a user. User should be given admin privileges
11. After installation, click reboot
12. After reboot, accept license information, then click finish configuration
13. At the initial set up, leave defaults on first two screens, turn off location services and skip connecting online accounts. 

NEXT, we will connect a repository and download CentOS packages and Elastic. 
1. From infrastructure laptop, open up WinSCP and open a connection to the device you are configuring. Drag and drop localrepo.repos from desktop directory on infrastructure laptop into the home directory of the Elastic VM, then close out the WinSCP Connection
2. Back in the VM, switch to super user (sudo su). IN the next few steps, run the commands as they appear in the steps
3. ping 10.1.7.30 (to ensure connectivity to the repository)
4. cd /etc
5. mkdir yum.repos.old
6. mv yum.repos.d/* yum.repos.old/
7. mv /home/gucci/localrepo.repo yum.repos.d/
8. ls yum.repos.old (to verify the old repos moved over)
9. ls yum.repos.d (to verify the only thing in there is localrepo.repo)
10. yum-config-manager --save --setopt=local-kit.skip_if_unavailable=true
11. yum repo-pkgs local-base install --skip-broken (if prompted, press 'y')
12. yum repo-pkgs local-extras install --skip-broken (if prompted, press 'y')
13. yum repo-pkgs local-updates install --skip-broken (if prompted, press 'y')
14. yum repo-pkgs local-centosplus install --skip-broken (if prompted, press 'y')
15. rpm --install "http://10.1.7.30/repos/kit/elasticsearch-7.10.2-x86_64.rpm"
16. cd /etc/elasticsearch
17. vim elasticsearch.yml
  WITHIN elasticsearch.yml, ALTER THE FOLLOWING, UNCOMMENT ANY LINES THAT ARE ALTERED
  - set the cluster name (this can be whatever you want)
  - set node name "node.name: nodex" where 'x' is the node number
  - set node attributes under the line "#node.attr.rack: r1" as follows:
    + node.master: true (only for the first node. other nodes set to false)
    + node.data: true
  - set network.host: 10.1.X.1x (e.g. network.host: 10.1.6.11)(ip of the VM)
  - set transport.port underneath line "For more information..." in network portion. Set it starting at 9300 with node1, incrementing by one for each node. (e.g. transport.port: 9300)
  - set the discovery seed hosts. discovery seed hosts will be the other nodes and their transport ports for this cluster. each line should be written with four spaces, then a hyphen, then another space. (e.g.    - 10.1.6.11:9300) enter a new line after entering each host
  - set cluster initial master nodes. this should just be the first node (e.g. cluster.initial_master_nodes: node1)
  - AT THE BOTTOM OF THE FILE, WRITE IN TWO LINES EXACTLY AS FOLLOWS
            #Shard limit for the entire node:
            cluster.routing.allocation.total_shards_per_node: 100
  - hit the escape key, then hit ":wq!" to save and exit the file.
18. vim jvm.options
  - change the XMS values from "-Xms1g" to "-Xms31g" for both Xms and Xmx.
  - hit the escape key, then hit ":wq!" to save and exit the file.
19. systemctl start elasticsearch
20. systemctl enable elasticsearch
21. firewall-cmd --add-port=5601/tcp --permanent
22. firewall-cmd --add-port=8005/tcp --permanent
23. firewall-cmd --add-port=9200/tcp --permanent
24. firewall-cmd --add-port=9300/tcp --permanent
25. firewall-cmd --add-port=9301/tcp --permanent
26. firewall-cmd --add-port=9302/tcp --permanent
27. firewall-cmd --add-port=9303/tcp --permanent
28. firewall-cmd --add-port=9304/tcp --permanent
29. systemctl status elasticsearch (to verify it is green and running)

FOR KIBANA, THIS SHOULD ONLY BE DONE ON THE MASTER NODE
1. rpm --install "http://10.1.7.30/repos/kit/kibana-7.10.2-x86_64.rpm"
2. cd /etc/kibana
3. vim kibana.yml (uncomment any edited lines)
  - set server.host to IP of the VM
  - set server.name to whatever you want
  - set elasticsearch.hosts just like the above discovery seed hosts with the same format, just as follows:
    + http://10.1.X.11:9200
    + http://10.1.X.12:9200
    + and so on
  - hit the escape key, the hit ":wq!" to save and exit the file
4. systemctl start kibana
5. systemctl enable kibana
6. systemctl status kibana (to ensure it is green and running)
