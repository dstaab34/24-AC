firewall-cmd --add-port=5601/tcp --permanent      5601, 8005, 9300, 9301, 9302, 9303, 9304
firewall-cmd --reload

$ curl -XGET 'localhost:9200/_cluster/health?pretty'
