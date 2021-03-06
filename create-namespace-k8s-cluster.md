- Create namespace by executing the following command
```
$ kubectl create ns dev
```

- Verify if the namespace is created by executing the command
```
$ kubectl get ns
```

- Create a yaml file for pod creation using vi editor
```
$ vi dev-nginx-pod.yaml
--- 
apiVersion: v1
kind: Pod
metadata:
  name: dev-nginx-pod
  namespace: dev
spec:
  containers:
  - name: nginx
    image: nginx:latest
```

- Save and exit the file

- Create pod using the yaml definition file by executing the command
```
$ kubectl apply -f dev-nginx-pod.yaml
```

- Verify if the pod is created by executing the command
```
$ kubectl get all -n dev
```