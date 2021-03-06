- Create a yaml file for deployment and service object creation using vi editor
```
$ vi nagios.yaml
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nagios-deployment
  labels:
    app: nagios
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nagios
  template:
    metadata:
      labels:
        app: nagios
    spec:
      containers:
      - name: nagios-container
        image: jasonrivers/nagios
---
apiVersion: v1
kind: Service
metadata:
  name: nagios-service
spec:
  selector:
    app: nagios
  type: NodePort
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
      nodePort: 30008
```
- Save and exit the file

- Create the deployment and service by executing the command
```
$ kubectl apply -f nagios.yaml
```

- Verify the deployment and service are created and all pods are in running state
```
$ kubectl get pods
$ kubectl get all
```

- Login into the nagios container using kubectl utility
```
$ kubectl exec -it nagios-deployment-6688dfbcfd-7wvs7 -- bash
```

- Verify the path where users are stored for the nagios core manager
```
$ cat /etc/apache2/sites-enabled/nagios.conf
```

- Create the user as requested in the question for login into nagios
```
$ htpasswd -c /opt/nagios/etc/htpasswd.users xFusionCorp
```

- Exit the container

- Click on the Nagios at the right hand side corner, enter the credentials configured in the previous step.
- You must be able to see the Nagios GUI