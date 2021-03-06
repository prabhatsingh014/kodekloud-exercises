- As the task required, run the following command to pull the nginx:alpine image from the docker hub repository.
```
$ sudo docker pull nginx:alpine
```

- Check whether the image has been pulled successfully
```
$ sudo docker images
```

- Create and run a container with name "media" and exposing the container port "80" on the host port "8088". Make sure the container is running in the background.
- Run the following command to accomplish this part of the task.
```
$ sudo docker run -d --name media -p 8088:80 nginx:alpine
```

- Check if the docker container is not running
```
$ sudo docker ps
```

- Note down the IP address of the host by running following command
```
$ ip addr
```

- Run the following command on the host to see if you're able to communicate on the exposed port
```
$ curl -v http://172.16.238.11:8088
```