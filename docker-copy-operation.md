- Login to the application server and switch to root user
- Run the docker ps command to check the running container
```
# docker ps
```

- Execute the docker cp command to copy the file on docker host to the container's directory
```
# docker cp /tmp/nautilus.txt.gpg ubuntu_latest:/home/
```

- Go to login shell of the container and verify if the file has been copied or not
```
# docker exec -it ubuntu_latest bash
# cd /home
# ls -ltr
```