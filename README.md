## Load Balance Solution with Apache

### This is an updated architecture to the tooling web solution by adding a Load Balancer to help with the distribution of incoming current traffic between two RHEL webservers. The final architecture includes 3-tier web application servers with a single MySQL database server, an NFS server + Load Balancer.


### The pre-requisite configuration includes the following:

#### 1. Apache (httpd) server is running on two web servers
#### 2. '/var/www' directories of both webserver are already mounted to '/mnt/apps' of the NFS server
#### 3. All necessary TCP/UDP ports are open on the Webservers, DB server and NFS server.
#### 4. Client browser can access both webservers public IPs on the web i.e. http://webserver1-publicIP/index.php