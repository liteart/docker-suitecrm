Docker SuiteCRM
===============

##About
This is a dockerized version of the SuiteCRM open source CRM. 
for the official github project please see here: https://github.com/salesagility/SuiteCRM

This project only prepares the existing SuiteCRM version for a easy to use Docker Development Image. This image is **not intended for production use!**


#Setup 

Best use this image with the official docker-mysql image. This has been tested and just works.

*Prerequisites:* A working docker environment

1. Setup the Mysql Server

   `docker run -d -e MYSQL_ROOT_PASSWORD=scrmdbpass -e MYSQL_DATABASE=suitecrm --name mysqlserver mysql:5.7`

2. Setup SuiteCRM. Enter the port you would like to expose
    
    `docker run -d -p 8020:80 --link mysqlserver bertschiweb/suitecrm`

3. Open your browser and enter the url `http://yourdockerserver:8020` 
    1. Accept the License Agreement
    2. Enter the Database configuration and Admin User Settings.
    
        ![alt text]("./docs/docs1.png")
        
        Attention: Make sure the database "Host Name" is the same as defined in the container link. eg. `mysqlserver``
        
    3. Click next and finish the setup assistant. 
    
4. Done!    



