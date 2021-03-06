- Create a yaml file with the following content for creating kubernetes replicaset.
- Ensure to verify the values of metadata.name, labels, replicas, selector, container name and image name.
```
$ vi httpd-replicaset.yaml
---
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: httpd-replicaset
  labels:
    app: httpd_app
    type: front-end
spec:
  replicas: 4
  selector:
    matchLabels:
      app: httpd_app
      type: front-end
  template:
    metadata:
      labels:
        app: httpd_app
        type: front-end
    spec:
      containers:
      - name: httpd-container
        image: httpd:latest
```     
- Save and exit the file.

- Execute the following command to create the kubernetes replicaset
```
$ kubectl apply -f httpd-replicaset.yaml
```

- Check the status of pods being created, until it starts running.
```
$ watch kubectl get pods
```