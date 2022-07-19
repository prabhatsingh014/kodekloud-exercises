- Task is to create persistent volume, then persistent volume claim, pod and at last server.
- At the end of the task completion, verification was supposed to done with the Web button at the top right hand corner.
- Important thing is to remember the documentRoot directory for httpd service i.e. /usr/local/apache2/htdocs. It needs to be configured correctly otherwise pod will crash.

- Execute the following command to create a file with all required kuberntes objects in the sequence.
```
$ vi datacenter.yaml
---
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: manual
provisioner: kubernetes.io/no-provisioner
volumeBindingMode: WaitForFirstConsumer
---
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-nautilus
  labels:
    app: web
spec:
  storageClassName: manual
  capacity:
    storage: 5Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: "/mnt/devops"
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pvc-nautilus
  labels:
    app: web
spec:
  storageClassName: manual
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 2Gi
---
apiVersion: v1
kind: Pod
metadata:
  name: pod-nautilus
  labels:
    app: web
spec:
  volumes:
    - name: pv-nautilus
      persistentVolumeClaim:
        claimName: pvc-nautilus
  containers:
    - name: container-nautilus
      image: httpd:latest
      volumeMounts:
        - mountPath: "/usr/local/apache2/htdocs"
          name: pv-nautilus
---
apiVersion: v1
kind: Service
metadata:
  name: web-nautilus
  labels:
    app: web
spec:
  type: NodePort
  selector:
    app: web
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30008
```
- Save and exit the file

- Execute the following command to create the kubernetes objects
```
$ kubectl apply -f datacenter.yaml
```

- Verify all kubernetes object are created successfully by executing following command
```
$ kubectl get pvc, pv, pod, svc
```

- Click on the Web GUI button on the top and you should be able to see the documentRoot with contect Index/