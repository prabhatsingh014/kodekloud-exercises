- Run the following command to create a network named blog with driver as macvlan, subnet as as 10.10.1.0/24 and IP range as 10.10.1.2/24.
```
$ sudo docker network create --driver macvlan --subnet 10.10.1.0/24 --ip-range 10.10.1.2/24 blog
```

- Once the network is created, verify the network details by running following commands.
```
$ sudo docker network ls    //List all networks
$ sudo docker inspect blog  //Display properties of the network "blog"
```