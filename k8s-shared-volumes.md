- Create a pod.yaml file with the name volume-share-nautilus and 2 containers using vi editor
```
$ vi pod.yaml
---
apiVersion: v1
kind: Pod
metadata:
  name: volume-share-nautilus
spec:
  containers:
  - name: volume-container-nautilus-1
    image: fedora:latest
    command: [ '/bin/sh', '-c', 'sleep 5000' ]
    volumeMounts:
    - name: volume-share
      mountPath: /tmp/news
  - name: volume-container-nautilus-2
    image: fedora:latest
    command: [ '/bin/sh', '-c', 'sleep 5000' ]
    volumeMounts:
    - name: volume-share
      mountPath: /tmp/demo
  volumes:
  - name: volume-share
    emptyDir: {}
```
- Save and exit the file

- Create the pod using the command
```
$ kubectl apply -f pod.yaml 
```

- Watch the pod creation using the command until it is running
```
$ kubectl get pod --watch
```

- Login to the first container of the pod and create the empty file
```
$ kubectl exec -it volume-share-nautilus -c volume-container-nautilus-1 -- bash
# cd /tmp/news/
# touch news.txt
# ls -ltr
```

- Exit from the first container and login to the second container to verify the file is present in the second container too
```
$ kubectl exec -it volume-share-nautilus -c volume-container-nautilus-2 -- bash
# ls -ltr /tmp/demo/
```