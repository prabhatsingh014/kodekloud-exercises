# Verify the puppetserver and puppet service status on both jump host and application server using root user
# # systemctl status puppetserver // to be run on jump host
# # systemctl status puppet // to be run on application server

- You may notice error in the puppet service status on application server on executing the status command
```
Error: couldn't connect to http://puppet:8140/......
```

- To resolve the issue, edit /etc/hosts file on both jump host and application server and append hostname "puppet" against jump host entries
```
# vi /etc/hosts
172.12.238.3 jump_host.stratos.xfusioncorp.com puppet
```
- Save and exit the file

- Restart the puppetserver service on jump host first
```
# systemctl restart puppetserver
```

- Restart the puppet service on application server
```
# systemctl restart puppet
```

- Once the services are restarted on both the nodes, check the signing request on the jump host using the command
```
# puppetserver ca list --all
```

- Sign the CSR requests using the command
```
# puppetserver ca sign --all
```

With this, your task is completed.