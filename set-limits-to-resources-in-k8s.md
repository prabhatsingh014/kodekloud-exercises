- Create a pod definition file with the requested resources limits and request using vi editor
```
$ vi httpd-pod.yaml

apiVersion: v1
kind: Pod
metadata:
  name: httpd-pod
spec:
  containers:
  - name: httpd-container
    image: httpd:latest
    resources:
      requests:
        memory: "15Mi"
        cpu: "100m"
      limits:
        memory: "20Mi"
        cpu: "100m"
```
- Save and exit the file

- Execute the following command to create the pod
```
$ kubectl apply -f httpd-pod.yaml
```

- Execute the following command to monitor the state of the pod creation until it is Running
```
$ watch kubectl get pods
```

- Execute the following command to describe the pod specification and see if the resource limits and requests are getting reflected correctly
```
$ kubectl describe pod httpd-pod
```