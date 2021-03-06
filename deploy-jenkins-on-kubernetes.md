- Create the jenkins namespace, deployment, and service objects creation yaml file
```
$ vi jenkins.yaml
---
apiVersion: v1
kind: Namespace
metadata:
  creationTimestamp: null
  name: jenkins
spec: {}
status: {}
---
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: jenkins
  name: jenkins-deployment
  namespace: jenkins
spec:
  replicas: 1
  selector:
    matchLabels:
      app: jenkins
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: jenkins
    spec:
      containers:
      - image: jenkins/jenkins
        name: jenkins-container
        ports:
        - containerPort: 8080
        resources: {}
status: {}
---
apiVersion: v1
kind: Service
metadata:
  creationTimestamp: null
  labels:
    app: jenkins
  name: jenkins-service
  namespace: jenkins
spec:
  type: NodePort
  ports:
  - port: 8080
    nodePort: 30008
    protocol: TCP
    targetPort: 8080
  selector:
    app: jenkins
status:
  loadBalancer: {}
```
- Save and exit the file

- Execute the command to create the objects
```
$ kubectl apply -f jenkins.yaml
```

- Verify if all objects have been created properly
```
$ kubectl get all -n jenkins
```