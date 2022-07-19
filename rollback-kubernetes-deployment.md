- To rollback kubernetes deploymen to the previous version.

- Check the rollout history by using following command.
```
# kubectl rollout history deployment/nginx-deployment
```

- Rollback to the previous version of the deployment by following command.
```
# kubectl rollout undo deployment/nginx-deployment
```

- Check the status of deployment (pods)
```
# watch kubectl get pods // you'll notice pods terminating and new pods coming up.
```