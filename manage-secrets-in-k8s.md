- Create the generic secret named offical using below command
```
$ kubectl create secret generic official --from-file=/opt/official.txt
```

- Verify if the secret has been created correctly with correct content
```
$ kubectl get secret
$ kubectl describe secret official
```

- Create a pod definition file named pod.yaml using vi editor
```
$ vi pod.yaml
---
apiVersion: v1
kind: Pod
metadata:
  name: secret-xfusion
  labels:
    name: secret-xfusion
spec:
  volumes:
  - name: secret-volume
    secret:
      secretName: official
  containers:
  - name: secret-container-xfusion
    image: ubuntu:latest
    command: [ "/bin/sh", "-c", "sleep 3600" ]
    volumeMounts:
    - name: secret-volume
      readOnly: true
      mountPath: "/opt/apps"
```
- Save and exit the file

- Create the pod using below command
```
$ kubectl create -f pod.yaml 
```

- Monitor the pod creation using following command until it is in "Running" state
```
$ kubectl get pods --watch
```

- Login to the pod using following command and verify the existence of the secret at the respective location
```
$ kubectl exec -it secret-xfusion -- bash
# ls -l /opt/apps/
```