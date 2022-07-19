- Execute the following command to identify the errors with the yaml file
```
$ kubectl apply -f mysql_deployment.yml 
```

- You may notice errors with the yaml related to :
a. identation
b. apiVersion
c. labels
d. requests.storage
e. matchLabels
f. array/list
g. image

- Once all the errors are rectified in the yaml, execute the kubectl apply command
- Verify if all resources are created using below command
```
$ kubectl get pv,pvc,svc,deployment
```