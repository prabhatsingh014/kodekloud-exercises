- Pod named webserver is configured with 2 containers, one is nginx container with image nginx:latest image and the other is sidecar container with image ubuntu:latest

- Verify the status of the pod by running the following command
```
$ kubectl get pods
```

- Status shows that one of the pod is not running and instead of showing Running status, it shows ImagePullBackOff
- Describe the pod with the following command
```
$ kubectl describe pod webserver
```

- Describe output shows the event with the content "failed to pull image nginx:latests"
- Notice the extra "s" in the image name in "latests"

- Generate the pod yaml file by executing the following command
```
$ kubectl get pod webserver -o yaml > webserver.yaml
```

- Edit the yaml file and correct the image name using vi editor
```
$ vi webserver.yaml
image: nginx:latests --> image: nginx:latest
```

- Save and exit the file

- Delete the existing pod by executing the following command
```
$ kubectl delete pod webserver
```

- Once the pod is delete, create the pod again using the yaml file
```
$ kubectl apply -f webserver.yaml
```

- Watch the pod status by executing the following command
```
$ kubectl get pods --watch
```