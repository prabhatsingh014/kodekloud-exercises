- Check what all pods, deployment, services are running on the k8s cluster
```
$ kubectl get all
```

- Check the deployment definition on how it's created
```
$ kubectl get deployment <deployment-name> -o yaml
```

- Check the service definition
```
$ kubectl get svc <service-name> -o yaml
```

- Check the config map 
```
$ kubect get cm <configmap-name> -o yaml
```

- Once you try to access the nodeport <30008>, it shows error bad gateway

- On analysing, it is found out that the issue is happening because of two issues
a. In service definition, targetPort is not correct
b. In configmap definition, index.php is either not correct or not defined at all

- Correct the targetPort in service object using the command
```
$ kubectl edit svc <service-name>
```

- Correct the index.php file name in the configmap using the command
```
$ kubectl edit cm <configmap-name>
```

- Once both are corrected, delete the existing pod. A new pod will automatically be created as it's part of a replica
```
$ kubectl delete pod <pod-name>
```

- Copy the index.php file from the host to the container as asked in the question
```
$ kubectl cp /tmp/index.php <pod-name>:/var/www/html -c nginx-container
```

- You should now be able to access the page at the nodePort 30008