- Create job definition file with name countdown-datacenter with the below content. Ensure to use "metadata" under spec.template.
```
$ vi countdown-datacenter.yaml
---
apiVersion: batch/v1
kind: Job
metadata:
  name: countdown-datacenter
spec:
  template:
    metadata:
      name: countdown-datacenter
    spec:
      containers:
      - name: container-countdown-datacenter
        image: debian:latest
        command: [ "/bin/sh", "-c", "for i in 10 9 8 7 6 5 4 3 2 1 0; do echo $i; done" ]
      restartPolicy: Never
```
- Save and exit the file

- Create the job object with the below command
```
$ kubectl apply -f countdown-datacenter.yaml
```

- Verify the job object creates the pods to execute the job command and gets completed
```
$ watch kubectl get pods
```

- Verify the logs of the pod to check if the command has executed perfectly
```
$ kubectl logs <pod-name>
```