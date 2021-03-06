- Create the namespace as requested in the question
```
$ kubectl create ns httpd-namespace-devops
```

- Verify the namespace has been created
```
$ kubectl get ns
```

- Create the deployment yaml file named httpd-deployment-devops.yaml with the specs mentioned in the task
- Ensure to include the namespace in which deployment is supposed to be created
```
$ vi httpd-deployent-devops.yaml
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: httpd-deployment-devops
  namespace: httpd-namespace-devops
  labels:
    app: web
spec:
  replicas: 2
  selector:
    matchLabels:
      app: web
  template:
    metadata:
      labels:
        app: web
    spec:
      containers:
      - name: httpd
        image: httpd:latest
```
- Save and exit the file

- Create the deployment by executing the following command
```
$ kubectl apply -f httpd-deployent-devops.yaml
```

- Verify the deployment is created using following command
```
$ kubectl get pods -n httpd-namespace-devops
```

- Create the service yaml file named httpd-service-devops.yaml with the following content
- Ensure to create the NodePort service
```
$ vi httpd-service-devops.yaml
---
apiVersion: v1
kind: Service
metadata:
  name: httpd-service-devops
  namespace: httpd-namespace-devops
spec:
  selector:
    app: web
  type: NodePort
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
      nodePort: 30004
```
- Save and exit the file

- Create the service using following command
```
$ kubectl create -f httpd-service-devops.yaml 
```

- Verify all the resource created in the namespace
```
$ kubectl get all -n httpd-namespace-devops
```