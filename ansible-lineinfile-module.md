- Create playbook.yaml on the jump host using vi editor
```
$ vi ~/ansible/playbook.yml
---
- hosts: all
  become: yes
  tasks:
  - name: Install httpd server on all app servers
    yum:
      name: httpd
      state: installed
  - name: Start httpd service on all app servers
    systemd:
      name: httpd
      state: started
      enabled: yes
  - name: Create index.html on all app servers
    file:
      path: /var/www/html/index.html
      state: touch
      owner: apache
      group: apache
      mode: 0644
  - name: Add content in index.html using shell module
    shell: echo "This is a Nautilus sample file, created using Ansible!" > /var/www/html/index.html
  - name: Add content in index.html using lineinfile module
    lineinfile:
      path: /var/www/html/index.html
      insertbefore: BOF
      line: 'Welcome to xFusionCorp Industries!'
```
- Save and exit the file

- Run the ansible playbook using ansible-playbook command
```
$ ansible-playbook -i ~/ansible/inventory ~/ansible/playbook.yml
```

- Once the playbook is finished, check the ownership and permission of index.html file using ansible adhoc command
```
$ ansible all -m shell -a 'ls -l /var/www/html/index.html' -i ~/ansible/inventory 
```

- Check the content of the index.html file using ansible adhoc command
```
$ ansible all -m shell -a 'cat /var/www/html/index.html' -i ~/ansible/inventory
```