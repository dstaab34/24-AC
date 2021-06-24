## AC Build
### Software
- Elasticsearch
- Kibana
- Arkime
- PFSense
- [VMware ESXi](https://github.com/dstaab34/24-AC/blob/main/ESXi.md)
- Rufus
- OpenOffice or Microsoft Suite
- BitVise
- WinSCP
### Wiping existing configuration
- [Click Here](https://github.com/dstaab34/24-AC/blob/main/WipeRaid.md) 
### Installing Operating systems
- [Click Here](https://github.com/dstaab34/24-AC/blob/main/BOOT.md)
### Creating Repo
- Download CentOS7 Repo
- Create CentOS7 VM on VMHost (25GB RAM, 50GB Storage)
- Install webserver application on VM (NGENX)
- Set up Repo on VMHost
- Set up Repo on Clients
### Elastic
## [Detailed Instructions](https://github.com/dstaab34/24-AC/blob/main/Elastic_Setup.md)
- Download Elastic RPM
- Install RPM on as many VMs as you think you need (odd #)(64GB RAM, 31GB Heap)
  - Storage for each node is generally the amount of PCAP you can store divided by 10 but can be more
- Configure elasticsearch.yaml
  - Sets IPs, Ports, Names, Clusters (NOTE: Max shards per node=100 may cause problems)
- Configure jvm.options file
  - Change heap size to 21
- Ensure cluster can communicate with each other
  - Check to see if IPTables is preventing this
- Download Kibana on one of the elastic nodes
### Moloch (Arkime)
- Install Moloch on Sensor
- Configure Moloch
  - IP to Geolocation file and oui.txt (Touch file with correct name)
  - Config.ini
    - Set directory to store PCAP, Change PCAP read method to TPACKETV3 and High Performance Settings
