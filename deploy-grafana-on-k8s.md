- Create deployment and service with any grafana image with the following yaml and commands.
```
$ vi grafana-deployment.yaml
---
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: grafana
  name: grafana-deployment-nautilus
spec:
  selector:
    matchLabels:
      app: grafana
  template:
    metadata:
      labels:
        app: grafana
    spec:
      containers:
        - name: grafana
          image: grafana/grafana:7.5.2
          ports:
            - containerPort: 3000
              name: http-grafana
              protocol: TCP
```
- Save and exit the file
- Run following command to create the deployment
```
$ kubectl apply -f grafana-deployment.yaml
```

- Create service with any name with type as NodePort and nodePort set as given in the question.
```
$ vi grafana-service.yaml
---
apiVersion: v1
kind: Service
metadata:
  name: grafana
spec:
  ports:
    - port: 3000
      nodePort: 32000
      protocol: TCP
      targetPort: http-grafana
  selector:
    app: grafana
  type: NodePort
```

- Run following command to create the service
```
$ kubectl apply -f grafana-service.yaml
```