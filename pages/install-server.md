---
title: Installing ownCloud Servver
last_updated: 13/12/2016
sidebar: mydoc_sidebar
permalink: install-server.html
---

This section describes how to install ownCloud Server using the official ownCloud Docker image. The image has the following configuration features:
 - It works with a data volume on the host file system
 - It works with separate MariaDB and Redis containers
 - It exposes port 8080 for HTTP connection
 - It mounts the data and MySQL data directories on the host for persistent storage

The commands in the procedure are performed using Docker Compose as the command-line tool.

**Note** You must have internet access to perform this task.

To install the ownCloud Server Docker image, follow these steps:

1. Create a new project directory for the installation as in the following example:  
       
    ``````
    mkdir owncloud-docker-server    
    ``````
           
2. Change directory to the directory you created in step 1, for example:  
    
    ``````
    cd owncloud-docker-server   
    ``````

4. Download a copy of docker-compose.yml from the GitHub repository using the following command:
         
    ````
    wget https://raw.githubusercontent.com/owncloud-docker/server/master/docker-compose.yml    
    ``````
2. At the command line, create an environment configuration file named .env and configure the required settings as in the following example:    
       
    > cat << EOF > .env    
    OWNCLOUD_VERSION=10.0    
    OWNCLOUD_DOMAIN=localhost    
    ADMIN_USERNAME=admin    
    ADMIN_PASSWORD=admin    
    HTTP_PORT=8080    
    EOF    

    The settings you configure in the .env file are described in the following table:

    |attribute | Description | Example |
    | -------- | ----------- | ------- |
    | OWNCLOUD_VERSION | The version you are installing | latest |
    | OWNCLOUD_DOMAIN | The ownCloud domain | localhost | 
    | ADMIN_USERNAME | The username for administrator autentication | admin |
    | ADMIN_PASSWORD | The password for administrator authentication | 
    | HTTP_PORT | The HTTP port to bind to | 8080 |

3. build and start the container using the following command:     

    docker-compose up -d

3. Verify that all the containers started successfully by running the following command:
    
    ````
    docker-compose ps `
    ````  

    If successful, output displays similar to the following:

    > Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Command  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  State  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Ports   
    >     ____________________________________________________________________________________________________________________________________________________________________________________________    
    
    >server_db_1 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /usr/bin/entrypoint/bin/s …  &nbsp;&nbsp; Up                &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;3306/tcp    
    server_owncloud_1 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  /usr/local/bin/entrypoint …  &nbsp;&nbsp; Up    &nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0.0.0.0:8080->8080/tcp    
    server_redis_1  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    /bin/s6-svscan /etc/s6  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;      Up               &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 6379/tcp

In the example above, all three containers are running. You can now access ownCloud through port 8080 on the host machine.

**Note:** It can take several minutes after the containers start running for ownCloud to be fully functional. You can veryify the running status by running the following command:    

````        
docker-compose logs --follow
````
    

If you see a significant amount of information logging to the console, wait until output slows down before attempting to access the web UI. 





   