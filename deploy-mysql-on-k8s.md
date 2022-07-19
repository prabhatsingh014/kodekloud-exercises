- Create the directory on the host machine using the command
```
$ sudo mkdir /mnt/data
```

- Create the PV creation yaml file
```
$ vi mysql-pv.yaml
---
apiVersion: v1
kind: PersistentVolume
metadata:
  name: mysql-pv
spec:
  storageClassName: standard
  capacity:
    storage: 250Mi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: "/mnt/data"
```
- Save and exit the file

- Create the persistent volume using the command
```
$ kubectl apply -f mysql-pv.yaml
```

- Create the PVC creation yaml file
```
$ vi mysql-pv-claim.yaml
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: mysql-pv-claim
spec:
  storageClassName: standard
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 250Mi
```
- Save and exit the file

- Create the persistent volume claim using the command
```
$ kubectl apply -f mysql-pv-claim.yaml
```

- Create the secret mysql-root-pass using the command
```
$ kubectl create secret generic mysql-root-pass --from-literal=password=YUIidhb667
```

- Create the secret mysql-user-pass using the command
```
$ kubectl create secret generic mysql-user-pass --from-literal=username=kodekloud_tim --from-literal=password=YchZHRcLkL
```

- Create the secret mysql-db-url using the command
```
$ kubectl create secret generic mysql-db-url --from-literal=database=kodekloud_db2
```

- Create the deployment creation yaml file
```
$ vi mysql-deployment.yaml
---
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: db
  name: mysql-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: db
  template:
    metadata:
      labels:
        app: db
    spec:
      containers:
      - image: mysql
        name: mysql
        volumeMounts:
        - mountPath: "/var/lib/mysql"
          name: mysql-storage
        env:
        - name: MYSQL_ROOT_PASSWORD
          valueFrom:
            secretKeyRef:
              name: mysql-root-pass
              key: password
        - name: MYSQL_DATABASE
          valueFrom:
            secretKeyRef:
              name: mysql-db-url
              key: database
        - name: MYSQL_USER
          valueFrom:
            secretKeyRef:
              name: mysql-user-pass
              key: username
        - name: MYSQL_PASSWORD
          valueFrom:
            secretKeyRef:
              name: mysql-user-pass
              key: password
      volumes:
      - name: mysql-storage
        persistentVolumeClaim:
          claimName: mysql-pv-claim
```
- Save and exit the file

- Create the deployment using the command
```
$ kubectl apply -f mysql-deployment.yaml
```

- Create the service creation yaml file
```
$ vi mysql-service.yaml
---
apiVersion: v1
kind: Service
metadata:
  labels:
    app: db
  name: mysql
spec:
  ports:
  - port: 3306
    nodePort: 30007
    protocol: TCP
    targetPort: 3306
  selector:
    app: db
  type: NodePort
```
- Save and exit the file

- Create the service using the command
```
$ kubectl apply -f mysql-service.yaml
```

- Verify the object creation using the command
```
$ kubectl get pv,pvc,secret,service,deployment
```