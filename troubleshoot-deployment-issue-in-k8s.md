- Execute the command to see what all resources have been running on the k8s cluster
```
$ kubectl get all
```

- From the output, it is found that pod has been in the ContainerCreating state
```
$ kubectl get all
NAME                                    READY   STATUS              RESTARTS   AGE
pod/redis-deployment-8bdf985f7-krwlb    0/1     ContainerCreating   0          113s
```

- Check the events that have occurred during the creation of the pod
```
$ kubectl describe pod/redis-deployment-8bdf985f7-krwlb

Events:
  Type     Reason       Age                From               Message
  ----     ------       ----               ----               -------
  Normal   Scheduled    50s                default-scheduler  Successfully assigned default/redis-deployment-8bdf985f7-krwlb to kodekloud-control-plane
  Warning  FailedMount  18s (x7 over 50s)  kubelet            MountVolume.SetUp failed for volume "config" : configmap "redis-conig" not found
```

- It is found that the pod is unable to mount the configmap on the volume attached
- Check the configmap deployed in the k8s cluster
```
$ kubectl get configmap
```

- From the output of above command, it is found that the configmap name is redis-config, however, pod is trying to mount the configmap with the name 'redis-conig'

- Edit and correct the deployment with correct configmap name
```
$ kubectl edit deployment redis-deployment
```

- Once the deployment is edited, check the current status of the pod running
```
$ kubectl get pods --watch
```

- Again, it is found that the pod is in running state and that it's giving ImagePullErr in the status

- Check the events during the creation of the pod
```
$ kubectl describe pod/redis-deployment-8bdf985f7-krwlb

  Events:
  Type     Reason     Age                From               Message
  ----     ------     ----               ----               -------
  Normal   Scheduled  50s                default-scheduler  Successfully assigned default/redis-deployment-6589b5b779-5gkn8 to kodekloud-control-plane
  Normal   BackOff    20s (x2 over 48s)  kubelet            Back-off pulling image "redis:alpin"
  Warning  Failed     20s (x2 over 48s)  kubelet            Error: ImagePullBackOff
  Normal   Pulling    7s (x3 over 49s)   kubelet            Pulling image "redis:alpin"
  Warning  Failed     6s (x3 over 48s)   kubelet            Failed to pull image "redis:alpin": rpc error: code = NotFound desc = failed to pull and unpack image "docker.io/library/redis:alpin": failed to resolve reference "docker.io/library/redis:alpin": docker.io/library/redis:alpin: not found
  Warning  Failed     6s (x3 over 48s)   kubelet            Error: ErrImagePull
```

- It if found from the events the pod is trying to run container with the image name as "redis:alpin", which tell us that the image name is incorrect. It is supposed to be "redis-alpine"

- Edit the deployment again and configure the image name as "redis-alpine"
```
$ kubectl edit deployment redis-deployment
```

- Once the deployment is recreated, check the pods status
```
$ kubectl get pods --watch
```

- Now all pods should be up and running.