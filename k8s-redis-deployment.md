- Create configmap and deployment in a single file and apply the changes.
```
$ vi redis-deployment.yaml
---
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-redis-config
data:
  maxmemory: "2mb"
---
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: redis-deployment
  name: redis-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: redis-deployment
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: redis-deployment
    spec:
      containers:
      - image: redis:alpine
        name: redis-container
        ports:
        - containerPort: 6379
        resources:
          requests:
            cpu: "1"
        volumeMounts:
        - name: data
          mountPath: /redis-master-data
        - name: redis-config
          mountPath: /redis-master
      volumes:
      - name: data
        emptyDir: {}
      - name: redis-config
        configMap:
          name: my-redis-config
status: {}
```
- Save and exit the file

- Run the following command to deploy the Kubernetes objects.
```
$ kubectl apply -f redis-deployment.yaml
```

- Check the configmap created by executing following command
```
$ kubectl get cm
```

- Check the deployment created by executing following command
```
$ kubectl get deployment,pod,replicaset
```

Or
```
$ kubectl get all
```