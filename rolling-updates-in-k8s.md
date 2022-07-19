- Check which objects are currently running on the k8s cluster
```
$ kubectl get all
```

- Verify the image version and update strategy being used by the existing deployment
```
$ kubectl describe deployment nginx-deployment
```

- Edit the deployment to update the image version
```
$ kubectl edit deployment nginx-deployment
```

- Check whether pods have been create with the updated image version
```
$ kubectl get pods
```

- Verify the image version being used by the running pods
```
$ kubectl describe pod nginx-deployment-576b8f48fb-4lq4k | grep Image
```