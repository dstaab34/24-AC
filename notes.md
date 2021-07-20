firewall-cmd --add-port=5601/tcp --permanent      5601, 8005, 9300, 9301, 9302, 9303, 9304
firewall-cmd --reload

$ curl -XGET 'localhost:9200/_cluster/health?pretty'

/data/moloch/bin/node addUser.js -c ../etc/config.ini admin "Admin" admin -admin

/data/moloch/bin/moloch-capture --copy -r <_pcap file_> (moloch tcp replay command)(you have to include the "--copy" portion so that the pcap you are replaying get's copied into the pcap directory specified in the config.ini file, so full pcap is available for analysis.) 
