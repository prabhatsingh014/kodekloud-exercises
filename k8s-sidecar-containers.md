- Create multi-pod container, one is web server and other is so called sidecar which help in executing few important tasks.
```
$ vi webserver.yaml
---
apiVersion: v1
kind: Pod
metadata:
  name: webserver
spec:
  containers:
  - name: nginx-container
    image: nginx:latest
    volumeMounts:
    - mountPath: /var/log/nginx
      name: shared-logs
  - name: sidecar-container
    image: ubuntu:latest
    command: ["sh","-c","while true; do cat /var/log/nginx/access.log /var/log/nginx/error.log; sleep 30; done"]
    volumeMounts:
    - mountPath: /var/log/nginx
      name: shared-logs
  volumes:
  - name: shared-logs
    emptyDir: {}
```
- Save and exit the file

- Create the pod by following command
```
$ kubectl apply -f webserver.yaml
```

- Watch if pods are running
```
$ watch kubectl get pods
```

- Check the logs getting 'cat' by the sidecar-container
```
$ kubectl logs webserver sidecar-container
```