- List the images present in the docker registry by executing the following command
```
$ sudo docker images
```

- List the containers running by executing the following command
```
$ sudo docker ps
```

- Create an image with tag from the running container with following command
```
$ sudo docker commit ubuntu_latest cluster:datacenter
```

- Verify the image is created
```
$ sudo docker images
```