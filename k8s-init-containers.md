- Make an yaml file containing deployments details as mentioned in the question such as replicas, labels, name, volumeMounts, image, container-name & volumes.
- Sample deployment file can be creates using following command
```
$ kubectl create deployment ic-deploy-xfusion --image=fedora:latest --replicas=1 --dry-run=client -o yaml > ic-deploy-xfusion.yaml
```

- Edit the file and fill the required defails as per question.
```
$ vi ic-deploy-xfusion.yaml
---
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: ic-xfusion
  name: ic-deploy-xfusion
spec:
  replicas: 1
  selector:
    matchLabels:
      app: ic-xfusion
  template:
    metadata:
      labels:
        app: ic-xfusion
    spec:
      initContainers:
      - image: fedora:latest
        name: ic-msg-xfusion
        command:
        - '/bin/bash'
        - '-c'
        - 'echo Init Done - Welcome to xFusionCorp Industries > /ic/media'
        volumeMounts:
        - name: ic-volume-xfusion
          mountPath: /ic
      containers:
      - image: fedora:latest
        name: ic-main-xfusion
        command:
        - '/bin/bash'
        - '-c'
        - 'while true; do cat /ic/media; sleep 5; done'
        volumeMounts:
        - name: ic-volume-xfusion
          mountPath: /ic
      volumes:
      - name: ic-volume-xfusion
        emptyDir: {}
```
- Save and exit the file

- Implement the kubernets deployment using below command.
```
$ kubectl apply -c ic-deploy-xfusion.yaml
```

- Check the deployment status with the following command. It will show the pods, deployment, & replicaset status, if they're ready and running.
```
$ kubectl get all
```

- Check the logs of the pods to see if it's printing the same logs as mentioned in the question.
```
$ POD=`kubectl get pods -l 'app: ic-xfusion' -o jsonpath='{.items[1].metadata.name}'`
$ kubectl logs $POD
```

- It should display the logs.