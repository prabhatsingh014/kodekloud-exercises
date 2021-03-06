- Login to application server as root user and see if the image is available in the docker registry with the command
```
# docker images
```

- Save the docker image to archive (.tar) using command
```
# docker save --output media.tar media:xfusion
```

- Transfer the archive to application server 3 using the command
```
# scp -rp /var/tmp/media.tar banner@stapp03:/home/banner
```

- Login to application server 3 as root user, change the path and load the docker image into registry
```
# cd /home/banner
# docker load --input media.tar 
```

**Note: docker service may not be in running state on the application server

- Execute the command to start the service as root user
```
# systemctl start docker; systemctl status docker
```

- Verify the image is imported into docker registry using the command
```
# docker images
```