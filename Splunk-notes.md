## Splunk Notes
Big VMs will be Splunk Enterprise and Splunk Enterprise security to alocate resources to.
Using a 1:2 pCPU to vCPU ratio Splunk enterprise will have 64 vCPUs with 256GB RAM and Splunk Ent. Sec. will have 32 vCPUs with 128GB RAM. These will be the biggest VMs by far.
Bottom Blade Sensor can have either a base install of CentOS 7 with Zeek, Suricata, and the Forwarder (Splunk Universal Forwarder if possible)
OR you could use Security Onion with ELKomply.

### Software
- Splunk Enterprise
- Splunk Enterprise Security
- APTF
- Splunk Universal FWDer
- Zeek
- Suricata

### Splunk Enterprise
Utilizing a Single instance of Splunk enterprise there will be a search head and indexers (and a forwarder but that is on the sensor)
Splunk Enterprise will be using the bulk of the resources which is why it is getting half of the entire blade.
