# Login to application server 1 and switch to root user

- Execute the command to check the running docker container on the app server 1
```
# docker ps
```

- Execute the command to check the ip address of the container
```
# docker inspect kkloud | grep -i ipaddress
```

- Execute the command to login to the container using bash shell
```
# docker exec -it kkloud bash
```

- At the container shell, execute the command to update the apt repository first and install apache2 package
```
# apt-get update
# apt-get install apache2
```

- Once the apache2 package is installed, update the listen address and port of the apache2 service
```
# sed -i 's/Listen 80/Listen 127.0.0.1:8084/' /etc/apache2/ports.conf
# echo 'Listen 192.168.3.2:8084' >> /etc/apache2/ports.conf
# echo 'ServerName 127.0.0.1' >> /etc/apache2/apache2.conf
# echo 'ServerName 192.168.3.2' >> /etc/apache2/apache2.conf
```

- Once configured, restart the apache2 service and verify the serice status using the commands
```
# service apache2 restart
# service apache2 status
```

- Install net-tools to verify the ports and address of the apache2 service
```
# apt-get install net-tools
```

- Verify the apache2 service is listening to the correct port and binded to the correct addresses
```
# netstat -anp | grep :8084
```