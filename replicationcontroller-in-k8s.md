- Create an yaml file with the details given in the question for the replication controller.
- Ensure to use the correct labels, pod name, container name, and image name.
```
$ vi httpd-replicationcontroller.yaml
---
apiVersion: v1
kind: ReplicationController
metadata:
  name: httpd-replicationcontroller
spec:
  replicas: 3
  selector:
    app: httpd_app
    type: front-end
  template:
    metadata:
      name: httpd-container
      labels:
        app: httpd_app
        type: front-end
    spec:
      containers:
      - name: httpd-container
        image: httpd:latest
```
- Save and exit the file

- Apply the kubernetes object using below command
```
$ kubectl apply -f httpd-replicationcontroller.yaml
```

- Verify if the replication controller is created along with the required pods
```
$ kubectl get all
```

- Describe the replication controller to verify the details
```
$ kubectl describe rc httpd-replicationcontroller
```