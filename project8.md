## Configuring Apache as a Load Balancer

### Ubuntu Server EC2 Instance on AWS was created and the TCP port80 in the inbound rules opened to allow connection

### Apache Load Balance is installed next on the ubuntu server and configured to point traffic the load balance receives to two web servers
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



### Load balancing is then configured for two webservers (using their respective private IPs) with equal load factors. Also, the bytraffic method was used to implement the incoming load distributed equally between the two webservers according to the current traffic load.

`sudo vi /etc/apache2/sites-available/000-default.conf`

![lb-config](/images/load-balance-config.PNG)
