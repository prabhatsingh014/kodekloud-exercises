- In this exercise, first you're supposed to pull the nginx:latest image from docker hub repository, then run a container using the same image and mount host directory /opt/dba on the /tmp directory in the container
- Also you have to name the container as "beta" and copy the /tmp/sample.txt file to the /opt/dba directory
- Ensure that the sample.txt file is present in the container as well

- Run the following command to switch to root user. Sometimes you may face issue when running with sudo users
```
$ sudo su -
```

- Pull the image of nginx from docker hub repository using below command
```
$ docker pull nginx:latest
```

- Run the container using nginx image, mount host directory with name beta
```
$ docker run -d --name beta -v /opt/dba:/tmp nginx:latest
```

- Check if the container is running with the following command
```
$ docker ps
```

- Copy the sample.txt file from /tmp to /opt/dba directory on the host
```
$ cp /tmp/sample.txt /opt/dba/
```

- Check if the same file is present inside the container at the location
```
$ docker exec -it beta ls -l /tmp
```