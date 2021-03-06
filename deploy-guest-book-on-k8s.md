- Create a deployment definition file named redis-master.yaml with the requirements given in the task
```
$ vi redis-master.yaml
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: redis-master
  labels:
    app: back-end-master
spec:
  replicas: 1
  selector:
    matchLabels:
      app: back-end-master
  template:
    metadata:
      labels:
        app: back-end-master
    spec:
      containers:
      - name: master-redis-nautilus
        image: redis
        ports:
        - containerPort: 6379
        resources:
          requests:
            cpu: "100m"
            memory: "100Mi"
```
- Save and exit the file

- Create the deployment by executing the following command
```
$ kubectl apply -f redis-master.yaml
```

- Create a service definition file with name redis-master-service.yaml
```
$ vi redis-master-service.yaml
---
apiVersion: v1
kind: Service
metadata:
  name: redis-master
spec:
  selector:
    app: back-end-master
  ports:
    - protocol: TCP
      port: 6379
      targetPort: 6379
```
- Save and exit the file

- Create the service by executing the following command
```
$ kubectl apply -f redis-master-service.yaml
```

- Create a deployment definition file named redis-slave.yaml with the requirements given in the task
```
$ vi redis-slave.yaml
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: redis-slave
  labels:
    app: back-end-slave
spec:
  replicas: 2
  selector:
    matchLabels:
      app: back-end-slave
  template:
    metadata:
      labels:
        app: back-end-slave
    spec:
      containers:
      - name: slave-redis-nautilus
        image: gcr.io/google_samples/gb-redisslave:v3
        ports:
        - containerPort: 6379
        env:
        - name: GET_HOSTS_FROM
          value: dns
        resources:
          requests:
            cpu: "100m"
            memory: "100Mi"
```
- Save and exit the file

- Create the deployment by executing the following command
```
$ kubectl apply -f redis-slave.yaml
```

- Create a service definition file with name redis-slave-service.yaml
```
$ vi redis-slave-service.yaml
---
apiVersion: v1
kind: Service
metadata:
  name: redis-slave
spec:
  selector:
    app: back-end-slave
  ports:
    - protocol: TCP
      port: 6379
      targetPort: 6379
```
- Save and exit the file

- Create the service by executing the following command
```
$ kubectl apply -f redis-slave-service.yaml
```

- Create a deployment definition file with name frontend.yaml with the requirements given in the task
```
$ vi frontend.yaml
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: frontend
  labels:
    app: front-end
spec:
  replicas: 3
  selector:
    matchLabels:
      app: front-end
  template:
    metadata:
      labels:
        app: front-end
    spec:
      containers:
      - name: php-redis-nautilus
        image: gcr.io/google-samples/gb-frontend:v4
        ports:
        - containerPort: 80
        env:
        - name: GET_HOSTS_FROM
          value: dns
        resources:
          requests:
            cpu: "100m"
            memory: "100Mi"
```
- Save and exit the file

- Create the deployment by executing the following command
```
$ kubectl apply -f frontend.yaml
```

- Create a service definition file with name frontend-service.yaml
```
$ vi frontend-service.yaml
---
apiVersion: v1
kind: Service
metadata:
  name: frontend
spec:
  type: NodePort
  selector:
    app: front-end
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
      nodePort: 30009
```
- Save and exit the file

- Create the service by executing the following command
```
$ kubectl apply -f frontend-service.yaml
```

- Once all the deployment and services are created, verify once if all deployments and services are in the desired state
```
$ kubectl get all
```

- As per question, click on the "=" sign on the top right corner of the page, enter port number (nodePort) and click View Port.
- You should be able to see guest book page where you can enter your message and click on Submit.