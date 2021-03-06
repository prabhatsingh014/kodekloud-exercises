- Create a yaml file with the correct pod name, container name, image name, and environment variables as asked in the question.
```
$ vi envars.yaml
---
apiVersion: v1
kind: Pod
metadata:
  name: envars
spec:
  containers:
    - name: fieldref-container
      image: redis:latest
      command: [ "sh", "-c"]
      args:
      - while true; do
          echo -en '\n';
          printenv NODE_NAME POD_NAME;
          printenv POD_IP POD_SERVICE_ACCOUNT;
          sleep 10;
        done;
      env:
        - name: NODE_NAME
          valueFrom:
            fieldRef:
              fieldPath: spec.nodeName
        - name: POD_NAME
          valueFrom:
            fieldRef:
              fieldPath: metadata.name
        - name: POD_IP
          valueFrom:
            fieldRef:
              fieldPath: status.podIP
        - name: POD_SERVICE_ACCOUNT
          valueFrom:
            fieldRef:
              fieldPath: spec.serviceAccountName
  restartPolicy: Never
```
- Save and exit the file

- Create the pod using following command
```
$ kubectl apply -f envars.yaml 
```

- Monitoring the status of pod creation with the following command until it starts running
```
$ watch kubectl get pods
```

- Check the logs of the POD using following command
```
$ kubectl logs envars
```

- You can also run the printenv command by taking the shell of POD
```
$ kubectl exec -it envars -- sh
# printenv
```