- Create the configmap with the file nginx.conf with the modified parameters in nginx.conf
- Two ways to create the config:
a. Create the nginx.conf locally with the required values and create configmap using kubectl utility with --from-file option.
a.1 Execute the following command to create configmap
```
$ kubectl create configmap nginx-config --from-file=nginx.conf
```
b. Using vi editor, create the yaml file with the following content
```
$ vi nginx-config.yaml
---
apiVersion: v1
data:
  nginx.conf: |
    user  nginx;
    worker_processes  auto;

    error_log  /var/log/nginx/error.log notice;
    pid        /var/run/nginx.pid;


    events {
        worker_connections  1024;
    }


    http {
        include       /etc/nginx/mime.types;
        default_type  application/octet-stream;

        log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                          '$status $body_bytes_sent "$http_referer" '
                          '"$http_user_agent" "$http_x_forwarded_for"';

        access_log  /var/log/nginx/access.log  main;

        sendfile        on;
        #tcp_nopush     on;

        keepalive_timeout  65;

        #gzip  on;

        include /etc/nginx/conf.d/*.conf;
        server {
        listen       8095;
        listen  [::]:8095;
        server_name  localhost;

        location / {
            root   /var/www/html;
            index index.html index.htm index.php;
        }
      }
    }
kind: ConfigMap
metadata:
  creationTimestamp: null
  name: nginx-config
```
- Save and exit the file

- Execute the command to create the configmap
```
$ kubectl apply -f nginx-config.yaml
```

- Create the pod creation yaml file with the following content using vi editor
```
$ vi nginx-phpfpm.yaml
---
apiVersion: v1
kind: Pod
metadata:
  name: nginx-phpfpm
  labels:
    app: nginx
spec:
  containers:
  - name: nginx-container
    image: nginx:latest
    volumeMounts:
    - name: nginx-config-volume
      mountPath: /etc/nginx/nginx.conf
      subPath: nginx.conf
    - name: shared-files
      mountPath: /var/www/html
  - name: php-fpm-container
    image: php:7.2-fpm
    volumeMounts:
    - name: shared-files
      mountPath: /var/www/html
  volumes:
  - name: nginx-config-volume
    configMap:
      name: nginx-config
  - name: shared-files
    emptyDir: {}
```
- Save and exit the file

- Execute the command to create the pod
```
$ kubectl apply -f nginx-phpfpm.yaml
```

- Create the service creation yaml file using vi editor
```
$ vi nginx-service.yaml
---
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  type: NodePort
  selector:
    app: nginx
  ports:
    - protocol: TCP
      port: 8095
      targetPort: 8095
      nodePort: 30012
```
- Save and exit the file.

- Execute the command to create the service
```
$ kubectl apply -f nginx-service.yaml
```

- Verify if all the objects are created and running properly
```
$ kubectl get cm,pod,svc
```

- Execute the command to copy the file present on the host machine to the nginx-container in nginx-phpfpm pod
```
$ kubectl cp /opt/index.php nginx-phpfpm:/var/www/html/ -c nginx-container
```