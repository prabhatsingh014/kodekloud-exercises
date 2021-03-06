- Check the inventory file if it has the node details mentioned properly
```
$ cat /home/thor/ansible/inventory 
```

- Verify the archive is present at the given path
```
$ ls -l /usr/src/devops/
```

- Create a playbook with name playbook.yml at the location /home/thor/ansible
```
$ vi /home/thor/ansible/playbook.yml 
---
- hosts: all
  become: yes
  tasks:
  - name: Unarchive file on all app servers
    unarchive:
      src: /usr/src/devops/datacenter.zip
      dest: /opt/devops/
      owner: "{{ ansible_user }}"
      group: "{{ ansible_user }}"
      mode: 0644
```
- Save and exit the file

- Verify the playbook run using the following command to ensure the required changes are correct
```
$ ansible-playbook -i inventory playbook.yml --check
```

- Execute the playbook using following command
```
$ ansible-playbook -i inventory playbook.yml
```

- Verify the archive is successfully decompressed on all app servers
```
$ ansible all -m shell -a 'ls -l /opt/devops' -i inventory
```