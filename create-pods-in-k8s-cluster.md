- Create the pod creation yaml file with the following content using vi editor
```
$ vi pod.yaml
---
apiVersion: v1
kind: Pod
metadata:
  name: pod-nginx
  labels:
    app: nginx_app
spec:
  containers:
  - name: nginx-container
    image: nginx:latest
```
- Save and exit the file

- Execute the command to create the pod
```
$ kubectl apply -f nginx.yaml 
```

- Verify the pod status
```
$ kubectl get pods
```