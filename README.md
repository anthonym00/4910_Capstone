# Enterprise System Administration CAPSTONE
The purpose of this project was to use the culmination of of my studies and apply them in a project which will serve the purpose of gaining hands on knowledege to what I've learned
## Project Summary
This project was done in groups of three and a summary of the tasks were: 
  * *Remove any malicous data on the machines that were deployed to the team* -------------------------
  * *Establish a DNS server and use Active Directory* -------------------------------------------------
  * *Configure a network which was based on a preconfigured network structure*  DONE ++++++++++++++++++
  * *Configure machines to communicate with each other and establish internet connections*  DONE ++++++
  * Create three goods and three services
  * *Install and configure a database to work with the webserver* -------------------------------------
  * *Host a website which would sell these goods and services to customers* ---------------------------
  * Create backups of the database server
  * Deploy an email server which will be used to communicate with the customers
  * Have network monitoring software which will allow the team to identify threats / unusual traffic
  * Generate logs 
  * *Run vulnerability scans to determine the networks security* --------------------------------------


***The italized items were the tasks I was responsible for**


  **Expectations:**
  * Be resilient against hacking attempts (Red team) 
  * Handle traffic generated by customers (Orange team) 
  * Respond to customer inquiries
  * Complete orders 
## Networking
The image below was the network that was given to us. The IP addresses on the diagram weren't configured on the machines, they were reccomended IP addresses. 


![Default Network](https://github.com/me14606/4910_Capstone/blob/main/Images/network.png?raw=true)


The difficult part of networking was figuing out which interface was facing which way, the diagram above was deceptive/inaccurate which made it quite difficult to configure the network. 

> Our Network Diagram
![](https://github.com/me14606/4910_Capstone/blob/main/Images/our_network.png?raw=true)

My solution: 
 1. Configure the machines ip addresses and DNS servers (DNS explained in a later section)
> Screenshot of Windows Webserver IP configuration
![windows](https://github.com/me14606/4910_Capstone/blob/main/Images/windows_ip.png?raw=true)


> Screenshot of Red Hat Enterprise Linux IP configuration
![red hat](https://github.com/me14606/4910_Capstone/blob/main/Images/rhel_ip.png?raw=true)

 3. Configure router/firewall one device at a time
    - I would configure one interface at a time pinging to a device and vice versa to ensure proper configuration
 4. On the routers and firewall I would set up static routes to ensure proper routing of traffic through the different subnets
 ![](https://github.com/me14606/4910_Capstone/blob/main/Images/s_routes_LAN.png?raw=true)
 ![](https://github.com/me14606/4910_Capstone/blob/main/Images/s_routes_WAN.png?raw=true)
 5. Configure the firewall to allow all traffic for the development purposes
    - Firewall rules were created after development was complete and the network hardening phase started
 6. Configure NAT on the WAN router to allow traffic to flow out from our internal network
 ![](https://github.com/me14606/4910_Capstone/blob/main/Images/NAT_WAN.png?raw=true)
 7. Test all devices in every subnet including routers for connectivity internally and to the internet
    - Tools used: 
      -ping (using ip addresses) 
      -nslookup (resolve dns) 
      -curl
 8. Create snapshots of all machines (Backup) 
 
** At this point all devices can communicate with each other and can access the internet **

## Install and Config Database Server
I chose to use mySQL as the dtabase server as it is compatible with wordpress (mentioned in [website] section ) and also found it easier to debug any issues if I used a DBMS that I'm familiar with


 Installing mySQL on RHEL Client: 
  1. Using the documetation linked below I successfully set up mySQL on RHEL
     - [Installing mySQL on Red Hat Enterprise Linux](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/9/html/configuring_and_using_database_servers/assembly_using-mysql_configuring-and-using-database-servers)
  3. Create database that will be used strictly for the wordpress website that will host our products/services
  2. I wanted to create a seperate mySQL user so the webserver would be the only user who could have access to the database using the new user account
     - Using the link below I created a user account which is only accessible by a specific ip, in this case from the webservers ip address
       - [mySql Remote Access](https://www.digitalocean.com/community/tutorials/how-to-allow-remote-access-to-mysql)
  3. Give permissions to the webserver mySQL user to access the wordpress database
  4. On the Webserver machine verify proper configuration by using HeidiSQL
  []()
  []()






  
 
