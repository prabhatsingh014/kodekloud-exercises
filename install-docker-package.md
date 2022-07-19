- Follow the installation procedure from the docker documentation available at https://docs.docker.com/engine/install/centos/
- I preferred to install docker engine using the convenience script.
- The steps are as below.

- Execute the command to download the convenience script
```
$ curl -fsSL https://get.docker.com -o get-docker.sh
```

- Execute the command to run the script which will install the docker engine
```
$ sudo sh get-docker.sh
```

- Once the installation is complete, start the docker service using the command
```
# systemctl start docker.service
```

- Check the status of the docker service
```
# systemctl status docker.service
```

- Follow the procedure to install docker-compose on the application server
- Latest release of docker-compose can be found here https://github.com/docker/compose/releases

- Copy the link address of the latest release of Linux_x86_64 binary
```
# curl -L https://github.com/docker/compose/releases/download/v2.6.1/docker-compose-linux-x86_64 -o /usr/local/bin/docker-compose
```

- Add the execute permission to the docker-compose binary
```
# chmod +x /usr/local/bin/docker-compose
```

- Check the version of docker-compose
```
# docker-compose --version
```