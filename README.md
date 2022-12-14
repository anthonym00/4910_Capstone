# Enterprise System Administration: CAPSTONE
The purpose of this project was to use the culmination of my studies in a project which will allow me to apply what I learned in a hands on environment 





## Project Summary
This project was done in groups of three and a summary of the tasks were: 
  * *Establish a DNS server and use Active Directory*
  * *Configure a network which was based on a preconfigured network structure* 
  * *Configure machines to communicate with each other and establish internet connections* 
  * Create three goods and three services
  * *Install and configure a database to work with the webserver* 
  * *Host a website which would sell these goods and services to customers* 
  * Create backups of the database server
  * Deploy an email server which will be used to communicate with the customers
  * Have network monitoring software which will allow the team to identify threats / unusual traffic
  * Generate logs 
  * *Run vulnerability scans to determine the networks security* 


***The italized items were the tasks I was responsible for**


  **Expectations:**
  * Be resilient against hacking attempts (Red team) 
  * Handle traffic generated by customers (Orange team) 
  * Respond to customer inquiries
  * Complete orders 

## DNS / AD 
 1. Delete the domain that was deployed with the machine
 2. Create a new domain
 
 >w4u domain
 ![](https://github.com/me14606/4910_Capstone/blob/main/Images/dns.png?raw=true)
    
 3. Join all machines to the domain
 4. Delete all old Active Directory users
 5. Create unique usernames / passwords to identify each compter
 
 >Active Directory users
 ![](https://github.com/me14606/4910_Capstone/blob/main/Images/AD.png?raw=true)
 
 7. Sign into any Active Directory user using all machines to test functionality
 
 
 
 
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
 > LAN/WAN Router Static Routes
 ![](https://github.com/me14606/4910_Capstone/blob/main/Images/s_routes_LAN.png?raw=true)
 ![](https://github.com/me14606/4910_Capstone/blob/main/Images/s_routes_WAN.png?raw=true)
 5. Configure the firewall to allow all traffic for the development purposes
    - Firewall rules were created after development was complete and the network hardening phase started
 6. Configure NAT on the WAN router to allow traffic to flow out from our internal network
 > WAN NAT Configuration  
 ![](https://github.com/me14606/4910_Capstone/blob/main/Images/NAT_WAN.png?raw=true)
 7. Test all devices in every subnet including routers for connectivity internally and to the internet
    - Tools used: 
      -ping (using ip addresses) 
      -nslookup (resolve dns) 
      -curl
 8. Create snapshots of all machines (Backup) 
 
** At this point all devices can communicate with each other and can access the internet **

## Install and Configure the Database Server
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
  > Accessing mySQL hosted on database server from webserver machine
  ![](https://github.com/me14606/4910_Capstone/blob/main/Images/heidi_web.png?raw=true)
  
  > Success!
  ![](https://github.com/me14606/4910_Capstone/blob/main/Images/heidi_web2.png?raw=true)
  5. Installing wordpress on the webserver
     - No screenshots were taken for this step, but the tutorial below accurately explains the process I used
       - [Installing and configuring Wordpress on Windows IIS ](https://www.microhost.com/docs/tutorial/how-to-install-wordpress-on-iis-in-windows-server-2019/)
  6. Once complete, it was time to set up the website

## Website Setup 
Wordpress was used to create our website for its rapid development cycle, ease of use, support, and security
1. Choosing theme: 
> Deli theme
![Theme](https://github.com/me14606/4910_Capstone/blob/main/Images/wp_theme.png?raw=true)
2. Installing plugins
   - Plugins used: 
     - **Woocommerce**: Allows the user to add products through the admin panel and seamlessly add them to the website 
     - **WooCommerce Payments**: A payment processing plugin 
     - **Jetpack**: A required plugin for various plugins to work
     - **Contact Form 7**: Used to create contact forms 


3. Customizing website

> Home Page
![Home Page](https://github.com/me14606/4910_Capstone/blob/main/Images/home_page.png?raw=true)


4. Adding products/services

> Shop: Products/Services
![Products/Services](https://github.com/me14606/4910_Capstone/blob/main/Images/shop.png?raw=true)


5. Creating contact form

> Contact us form 
![Products/Services](https://github.com/me14606/4910_Capstone/blob/main/Images/contact.png?raw=true)

6. Test cart and checkout features for proper functionality
7. Test contact us form for proper functionality

***At this time the website is complete**

## Vulnerability Scans / Network Hardening
1. Run Vulnerability Scans
   - Theses Nmap scans were run from the kali machine on the WAN segment of the network
   - Due to the length of the reports they will be linked below
     - [Vulnerability Reports Before](https://github.com/me14606/4910_Capstone/tree/main/Vulnerablility%20Reports%20Before)

2. Close Ports
   -Every port was looked up to determine their usefulness per machine
    -If useful, make sure there were no vulnerabilities for the services running on the open ports
   -Verify port are closed on machine firewall
   __Some ports/services were only nesssary in their own subnet__
    -Ex) Database only needs one port open to the webserver
3. Create firewall rules for each subnet using Pfsense
   >WAN Firewall Rules
   ![Products/Services](https://github.com/me14606/4910_Capstone/blob/main/Images/wanfw.png?raw=true)
   ![Products/Services](https://github.com/me14606/4910_Capstone/blob/main/Images/wanfw2.png?raw=true)
   
   >LAN Firewall Rules
   ![Products/Services](https://github.com/me14606/4910_Capstone/blob/main/Images/lanfw.png?raw=true)
   
   >DMZ Firewall Rules
   ![Products/Services](https://github.com/me14606/4910_Capstone/blob/main/Images/dmzfw.png?raw=true)
   
4. Post-vulnerability scan to verify rules were applied successfully 


## Lessons Leaarned
   - Prior to this class I had trouble understanding how to route data to different subnets which werent directly accessible to a router 
     - Through reasearch and trial and error I understood routing works and the purpose of "next-hop"
   - Ive learned to secure all sides of a network, a strong network firewall doesn't suffice
     - Add device firewall rules
     - Close ports
     - Update systems
     - Encrypt traffic 
   
## What I would've changed
   - Task distribution could've been worked on 
   - Increased security at the device level 
   - Adding network Monitors
   - Adding Traffic monitors

##  Other Information / Documentation

>KANBAN
![Kanban](https://github.com/me14606/4910_Capstone/blob/main/Images/kanb.png?raw=true)

>What went well / What didn't go well 
![Products/Services](https://github.com/me14606/4910_Capstone/blob/main/Images/good_bad.png?raw=true)



>Tasks (Green were my responsibility) 
![Tasks](https://github.com/me14606/4910_Capstone/blob/main/Images/tasks.png?raw=true)
 
