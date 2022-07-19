- Create the inventory with the following content
```
$ vi /home/thor/playbook/inventory
stapp02 ansible_host=172.16.238.11 ansible_user=steve ansible_password=Am3ric@
```
- Save and exit the file

- Verify if the inventory is working for you by executing the following command
```
$ ansible stapp02 -m ping -i ~/playbook/inventory
```

- This may result in an error asking to add the host key in the known_hosts file on the jump host server
- For the purpose, try to SSH to stapp02 once with the username and password given
```
$ ssh steve02@stapp02
```

- This will add the host key in the known_hosts file

- Now execute the playbook again and you will be able to ping the stapp02 using ansible ad-hoc command
```
$ ansible stapp02 -m ping -i ~/playbook/inventory
```

- Task will check by executing the command, so make sure the run the following command
```
$ cd ~/playbook
$ ansible-playbook -i inventory playbook.yml
```