CONTINUING FROM BOOT.md CENTOS INSTRUCTIONS
1. During initial setup, click next, then click next, then turn off location services and click next, then click skip. 
2. From infrastructure laptop, open up WinSCP and open a connection to the device you are configuring with 'gucci' credentials. Drag and drop localrepo.repos from desktop directory on infrastructure laptop into the home directory of the Moloch Server, then close out the WinSCP Connection
3. Back in the iDrac console of the Moloch Server,Open up a terminal session by right clicking and selecting "open terminal"
4. switch to super user (sudo su). IN the next few steps, run the commands as they appear in the steps
5. ping 10.1.7.30 (to ensure connectivity to the repository)
6. cd /etc
7. mkdir yum.repos.old
8. mv yum.repos.d/* yum.repos.old/
9. mv /home/gucci/localrepo.repo yum.repos.d/
10. ls yum.repos.old (to verify the old repos moved over)
11. ls yum.repos.d (to verify the only thing in there is localrepo.repo)
12. yum-config-manager --save --setopt=local-kit.skip_if_unavailable=true
13. yum repo-pkgs local-base install --skip-broken (if prompted, press 'y')
14. yum repo-pkgs local-extras install --skip-broken (if prompted, press 'y')
15. yum repo-pkgs local-updates install --skip-broken (if prompted, press 'y')
16. yum repo-pkgs local-centosplus install --skip-broken (if prompted, press 'y')
17. yum localinstall "http://10.1.7.30/repos/kit/moloch-2.7.1-1.x86_64.rpm" (if prompted, press 'y')
18. cd /data/moloch
19. touch /data/moloch/etc/oui.txt
20. touch /data/moloch/etc/ipv4-address-space.csv
21. cd bin
22. ./Configure
  - type in "em3" when prompted to enter interfaces to monitor, then press enter
  - type in "no" when asked to install elasticsearch server locally, then press enter
  - type in elasticsearch server IP next, should be "http://10.1.X.11:9200", where 'X' is the subnet of the kit you are on (e.g. http://10.1.6.11:9200)
  - do not set password to encrypt, type in "no" and press enter
  - type in "no" when asked about downloading GEO files, then press enter
  - when configuration completes, ensure the elastic nodes on the same kit are up and running (systemctl status elasticsearch) (curl http://10.1.X.11:9200/_cat/health)
23. /data/moloch/db/db.pl http://10.1.X.11:9200 init
24. /data/moloch/bin/moloch_add_user.sh admin "Admin User" admin --admin (this will set the admin username and password to 'admin'. change later in the Moloch browser)
25. firewall-cmd --add-port=5601/tcp --permanent
26. firewall-cmd --add-port=8005/tcp --permanent
27. firewall-cmd --add-port=9200/tcp --permanent
28. firewall-cmd --add-port=9300/tcp --permanent
29. firewall-cmd --add-port=9301/tcp --permanent
30. firewall-cmd --add-port=9302/tcp --permanent
31. firewall-cmd --add-port=9303/tcp --permanent
32. firewall-cmd --add-port=9304/tcp --permanent
33. systemctl start molochviewer
34. systemctl start molochcapture
35. systemctl enable molochviewer
36. systemctl enable molochcapture
37. systemctl status molochviewer
38. systemctl status molochcapture 
39. init 6
40. systemctl status molochviewer
41. systemctl status molochcapture
42. Go into a browser on the infrastructure laptop, type in "http://10.1.X.20:8005" where 'X' is the kit subnet. Validate with the admin credentials set in step 24.
43. Click on stats tab, then click on "ES Nodes" and verify you have node1-node5 listed. 
