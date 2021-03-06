- Create the inventory with application server details using vi editor
```
$ vi /home/thor/ansible/inventory

stapp01 ansible_host=172.16.238.10 ansible_user=tony ansible_password=Ir0nM@n
stapp02 ansible_host=172.16.238.11 ansible_user=steve ansible_password=Am3ric@
stapp03 ansible_host=172.16.238.12 ansible_user=banner ansible_password=BigGr33n
```

- Save and exit the file

- Verify if your inventory is working without any issue by executing one sample command as below
```
$ ansible -m ping all -i inventory 
```

- Create plabyook.yml with task to copy file from jump host to application server using vi editor
```
vi /home/thor/ansible/playbook.yml
---
- hosts: all
  become: yes
  tasks:
  - name: Copy index.html to all application servers
    copy:
      src: /usr/src/itadmin/index.html
      dest: /opt/itadmin/
```
- Save and exit the file

- Run the playbook using command
```
$ ansible-playbook -i inventory playbook.yml
```

- Verify if the file has been copied over to application servers
```
$ ansible all -m shell -a 'ls -l /opt/itadmin' -i inventory
```