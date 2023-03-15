## Configuring Apache as a Load Balancer

### Step 1 - Ubuntu Server EC2 Instance on AWS was created for apache-Load-balance and the TCP port80 in the inbound rules opened to allow connection. Also, the dbserver, NFS server and two RHEL webservers were also setup and their instances started.

### Step 2 - Apache Load Balance is installed next on the ubuntu server and configured to point traffic the load balance receives to two web servers
`sudo apt update`
`sudo apt install apache2 -y`
`sudo apt-get install libxml2-dev`

![apache-install](/images/apache-install.PNG)

### Then, the following modules are enabled

`sudo a2enmod rewrite`

`sudo a2enmod proxy`

`sudo a2enmod proxy_balancer`

`sudo a2enmod proxy_http`

`sudo a2enmod headers`

`sudo a2enmod lbmethod_bytraffic`

![module-enable](/images/enabling-modules.PNG)


### Apache2 service restarted and ensured the apache2 is running

`sudo systemctl restart apache2`
`sudo systemctl status apache2`

![apache-run](/images/apache-run.PNG)



### Step 3 - Load balancing is then configured for two webservers (using their respective private IPs) with equal load factors. Also, the bytraffic method was used to implement the incoming load distributed equally between the two webservers according to the current traffic load.

`sudo vi /etc/apache2/sites-available/000-default.conf`

![lb-config](/images/load-balance-config.PNG)


### Step 4 - The test for the configuration is done by accessing the Load balance server Public IP address on the web

`http://<Load-Balancer-Public-IP-Address-or-Public-DNS-Name>/index.php`

![lb-web](/images/LB-web.PNG)


### Sequel to the previous project on devops web tooling solution, the `/var/log/httpd` mounted from the webservers to the NFS servers needs to be unmounted from the two webservers here.

`sudo tail -f /var/log/httpd/access_log`

### Then the webpage was refreshed several times to test the equal distribution of requests received on both webservers from the load balancer. It was observed that both webservers received equal requests as shown below.

![lb-web1](/images/webserver1-loadref.PNG)

![lb-web2](/images/webserver2-loadref.PNG)


### The next couple of steps are to configure local DNS names. i.e. renaming our two webservers IP address to a resolved name chosen. To achieve this, the `/etc/hosts` file needs to be updated and also the load Balance config file.

![dns-name](/images/dns-name.PNG)

![ipname](/images/lbconfig-ipname.PNG)

### Finally, to test the above steps, the webservers were both tested from the LB server.
`curl http://WebServer1`

![curlweb1](/images/curl-webserver1.PNG)


`curl http://WebServer2`

![curlweb2](/images/curl-webserver2.PNG)



