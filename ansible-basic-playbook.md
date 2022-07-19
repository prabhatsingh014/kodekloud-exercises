- Verify the inventory file and correct the host specific entries.
- In this case, IP of ansible_host

```
$ cat ~/ansible/inventory 
stapp01 ansible_host=172.16.238.10 ansible_user=tony
```

- Establish password-less connectivity between jump host and the application server
- First step is to generate the SSH keys on the jump host for thor user
```
$ cd ~/.ssh/
$ ssh-keygen -t rsa
```

- Copy the public key to the application server using ssh-copy-id command
```
$ ssh-copy-id -i id_rsa.pub tony@172.16.238.10
```

- Verify the ssh connectivity by logging into the application server
```
$ ssh tony@stapp01
```

- Create the ansible playbook using vi editor
```
$ vi ~/ansible/playbook.yml
---
- hosts: stapp01
  become: yes
  tasks:
  - name: Create an empty file
    file:
      name: /tmp/file.txt
      state: touch
```

- Save and exit the file

- Check whether the playbook implements the right changes on the application server
```
$ ansible-playbook -i ~/ansible/inventory ~/ansible/playbook.yml --check 
```

- Run the ansible playook using the command
```
$ ansible-playbook -i ~/ansible/inventory ~/ansible/playbook.yml
```

- Verify if the file has been created on the application server
```
$ ansible -m shell -a 'ls -l /tmp/file.txt' -i ~/ansible/inventory stapp01
```