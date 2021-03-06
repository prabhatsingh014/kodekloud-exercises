- Check the kubernetes cluster on the jump host server
```
$ kubectl get nodes
```

- Create namespace as mentioned in the question with the following command
```
$ kubectl create ns tomcat-namespace-nautilus
```

- Verify the creation of namespace
```
$ kubectl get ns
```

- Create the deployment and service definition in a yaml file as given below
```
$ vi tomcat-deployment-nautilus.yaml
---
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: tomcat
  name: tomcat-deployment-nautilus
  namespace: tomcat-namespace-nautilus
spec:
  replicas: 1
  selector:
    matchLabels:
      app: tomcat
  template:
    metadata:
      labels:
        app: tomcat
    spec:
      containers:
      - image: gcr.io/kodekloud/centos-ssh-enabled:tomcat
        name: tomcat-container-nautilus
        ports:
        - containerPort: 8080
---
apiVersion: v1
kind: Service
metadata:
  labels:
    app: tomcat
  name: tomcat-service-nautilus
  namespace: tomcat-namespace-nautilus
spec:
  ports:
  - port: 8080
    nodePort: 32227
    protocol: TCP
    targetPort: 8080
  selector:
    app: tomcat
  type: NodePort
```
- Save and exit the file

- Create the deployment and service objects by executing the following command
```
$ kubectl create -f tomcat-deployment-nautilus.yaml 
```

- Verify the creation of kubernetes objecte by executing the following command
```
$ kubectl get all -n tomcat-namespace-nautilus
```