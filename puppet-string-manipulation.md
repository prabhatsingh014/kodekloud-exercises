- Ensure that puppetserver and puppet agent services are running on master and agent nodes
- Run the following command to verify the service status on Puppet Master
```
$ sudo systemctl status puppetserver
```
- On Puppet Agent
```
$ sudo systemctl status puppet
```

- Once that's verified, create the manifest file
```
$ cd /etc/puppetlabs/code/environments/production/manifests
$ sudo vi cluster.pp

node 'stapp03.stratos.xfusioncorp.com' {
}

file_line { 'replaceline':
  ensure => present,
  path => '/opt/data/apps.txt',
  line => 'Welcome to xFusionCorp Industries!',
  match => 'Welcome to Nautilus Industries!',
}
```
- Save and exit file

- On puppet agent node, run the command with sudo, if using non-root user.
```
$ sudo puppet agent -tv
```

- Once command is executed, verify the file content on the agent node.
```
$ cat /opt/dba/cluster.txt 
```