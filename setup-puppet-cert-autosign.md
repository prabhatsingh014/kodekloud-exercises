- Verify puppetserver and puppet services are running on the master and agent nodes.
- To verify service puppetserver on master node, run following command.
```
$ systemctl status puppetserver
```

- To verify service puppet on the agent nodes, run following command.
```
$ systemctl status puppet
```

- Update the /etc/hosts file on the master and agent nodes with the name "puppet" appended to the master node entry.
```
$ vi /etc/hosts
172.16.238.3 jump_host.stratos.xfusioncorp.com jump_host puppet
```
- Save the file

- Create autosign.conf file under /etc/puppetlabs/puppet directory on the puppet master node.
```
$ vi /etc/puppetlabs/puppet/autosign.conf
jump_host@stratos.xfusioncorp.com
stapp01.stratos.xfusioncorp.com
stapp02.stratos.xfusioncorp.com
stapp03.stratos.xfusioncorp.com
```
- Save the file

- Edit the puppet.conf file under /etc/puppetlabs/puppet directory on the puppet master node.
```
$ vi /etc/puppetlabs/puppet/puppet.conf
```

- Add followign line in the file
```
autosign = /etc/puppetlabs/puppet/autosign.conf
```

- Save the file

- Restart the puppetserver service on the puppet master node
```
$ systemctl restart puppetserver
```

- Check the puppetserver service status on the puppet master node
```
$ systemctl status puppetserver
```

- Check the puppetserver ca list on the puppet master node
```
$ puppetserver ca list --all
```

- Output shoulld display ca entry of the master node

- Restart the puppet service on the puppet agent nodes
```
$ systemctl restart puppet
```

- Check the puppet service status on the puppet agent nodes
```
$ systemctl status puppet
```

- Test the changes on the puppet agent nodes
```
# puppet agent -tv
```

- Check the puppetserver ca list on the puppet master node
```
$ puppetserver ca list --all
```

- Output should display ca entry of the master and agent nodes