- Check the status of the deployment, pods, services running on the kubernetes cluster
```
$ kubectl get all
```

- Check the events of pod creation
```
$ kubectl describe pod <podname>
```

- Error "ImagePullError" is being displayed in the events
- Verify the image name being used in the deployment creation
```
$ kubectl describe deployment <deploymentname>
```

- Correct the image name using the command
```
$ kubectl edit deployment <deploymentname>
```

- This will recreate the pods and watch the status of the pod until it is running
```
$ kubectl get pods --watch
```

- Check the service configuration
```
$ kubectl describe svc <servicename>
```

- Edit and correct the service configuration using the command
```
$ kubectl edit svc <servicename>
```

- Click on the App icon on the right hand side corner of the page.
- You must be able to see the page content