- Create the ecommerce.pp file at the specified location on the puppet master node i.e. jump host using vi editor
```
$ vi /etc/puppetlabs/code/environments/production/manifests/ecommerce.pp 
node 'stapp02.stratos.xfusioncorp.com' {
}

user { 'siva':
  ensure   => present,
  uid      => 1804,
}
```
- Save and exit the file

- Login to stapp02 application server and switch to root user
```
$ sudo su -
```

- Execute the following command to implement the changes
```
# puppet agent -tv
```

- Verify if the user is create on stapp02 node
```
$ grep siva /etc/passwd
```