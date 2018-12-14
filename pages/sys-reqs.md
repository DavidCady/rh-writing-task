---
title: System Requirements
last_updated: 13/12/2016
sidebar: mydoc_sidebar
permalink: sys-reqs.html
---

The host machine you use to install and run ownCloud must have the following minimum specifications:

    * Two CPU cores
    * 16GB RAM
    * Local storage as required


The following are the recommended software requirements for running ownCloud server in a single-server deployment:
                   
- **Operating system:**
    - Red Hat Enterprise Linux/Centos 6.9, 7.3, 7.4, and 7.5   
    **Note:** Red Hat Enterprise Linux & Centos 7 are 64-bit only 
    
    - SUSE Linux Enterprise Server 12 with SP1, SP2 and SP3    



- **Database:**
    - MySQL   
    **Note:** SQLite is not encouraged for production use.
    - MariaDB 5.5 or higher.   
    **Note** With either dataase you must use the InnoDB storage engine because MyISAM is not supported.

- **Webserver:**
    - Apache 2.4 with prefork apache-mpm-label and mod_php

- **Scripting Language Package:**
-     - PHP5.6 or higher
 
 
Cron access

SSL Configuration
The SSL termination is done in Apache. A standard SSL certificate is required to be installed according to the official Apache documentation.
  


