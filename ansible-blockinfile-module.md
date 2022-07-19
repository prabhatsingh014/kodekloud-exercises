- Create playbook.yml using vi editor
```
$ vi ~/ansible/playbook.yml
---
- hosts: all
  become: yes
  tasks:
  - name: Install httpd service
    yum:
      name: httpd
      state: present
  - name: Start httpd service
    systemd:
      name: httpd
      state: started
      enabled: yes
  - name: Add content in index.html
    blockinfile:
      path: /var/www/html/index.html
      block: |
        Welcome to XfusionCorp!
        This is Nautilus sample file, created using Ansible!
        Please do not modify this file manually!
      owner: apache
      group: apache
      mode: 0655
      create: yes
```

- Save and exit the file

- Execute the command to run the playbook
```
$ ansible-playbook -i inventory playbook.yml
```

- Execute the command to verify the content of index.html
```
$ ansible all -m shell -a 'cat /var/www/html/index.html' -i inventory 
```

- Execute the command to verify the permission and ownership of the file
```
$ ansible all -m shell -a 'ls -l /var/www/html/index.html' -i inventory
```