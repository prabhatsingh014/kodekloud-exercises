- Create yaml file consisting of job definition using vi editor
```
$ vi countdown-devops.yaml
---
apiVersion: batch/v1
kind: Job
metadata:
  name: countdown-devops
spec:
  template:
    metadata:
      name: countdown-devops
    spec:
      containers:
      - name: container-countdown-devops
        image: ubuntu:latest
        command: ["/bin/sh", "-c", "for i in 10 9 8 7 6 5 4 3 2 1 ; do echo $i ; done"]
      restartPolicy: Never
```
- Save and exit the file

- Create the job using the command
```
$ kubectl apply -f countdown-devops.yaml
```

- Monitor the status of the pod until it starts running or completed
```
$ kubectl get pods --watch
```

- Check the logs of the POD if the countdown is displayed
```
$ kubectl logs countdown-devops-f5xv6
```