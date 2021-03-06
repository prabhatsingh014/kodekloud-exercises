- Create the yaml template for the deployment named nginx with image nginx:latest
```
$ kubectl create deployment nginx --image=nginx:latest --dry-run=client -o yaml

apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: nginx
  name: nginx
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: nginx
    spec:
      containers:
      - image: nginx:latest
        name: nginx
        resources: {}
status: {}

$ kubectl create deployment nginx --image=nginx:latest --dry-run=client -o yaml > nginx.yaml
```

- Create the deployment using below command
```
$ kubectl create deployment nginx --image=nginx:latest
```

- Watch the status of pods until it is in "Running" state
```
$ kubectl get pods --watch
```