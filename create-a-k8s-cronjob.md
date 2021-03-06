- Create the cronjob creation yaml file using vi editor
```
$ vi hello.yaml
---
apiVersion: batch/v1
kind: CronJob
metadata:
  name: hello
spec:
  schedule: "* * * * *"
  jobTemplate:
    spec:
      template:
        spec:
          containers:
          - name: hello
            image: busybox
            imagePullPolicy: IfNotPresent
            command:
            - /bin/sh
            - -c
            - date; echo Hello from the Kubernetes cluster
          restartPolicy: OnFailure
```
- Save and exit the file

- Execute the command to create the cronjob object
```
$ kubectl apply -f hello.yaml
```

- Verify the cronjob creation
```
$ kubectl get cronjob hello
```

- Check the logs of the cronjob
```
$ kubectl logs hello
```