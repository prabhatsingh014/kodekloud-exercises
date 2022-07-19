- Verify the inventory file create at the location /home/thor/ansible/playbooks
```
$ cat /home/thor/ansible/playbooks/inventory
```

- Create httpd.yml to setup httpd and php on the target application server, in this case, stapp02
```
$ vi ~/playbooks/httpd.yml
---
- hosts: stapp02
  become: yes
  tasks:
  - name: Install httpd and php
    yum:
      name: ['httpd', 'php']
      state: present

  - name: Create directory if it does not exist
    file:
      path: /var/www/html/myroot
      state: directory

  - name: Change default document root
    lineinfile:
      path: /etc/httpd/conf/httpd.conf
      regexp: '^DocumentRoot'
      line: 'DocumentRoot /var/www/html/myroot'

  - name: Copy template to document root
    template:
      src: ~/playbooks/templates/phpinfo.php.j2
      dest: /var/www/html/myroot/phpinfo.php
      owner: apache
      group: apache

  - name: Start httpd service
    systemd:
      name: httpd
      state: started
      enabled: yes
```
- Save and exit the file

- Verify if the changes implemented by the playbook are correct by executing the command
```
$ ansible-playbook -i ~/playbooks/inventory httpd.yml --check
```

- Run the playbook by executing the command
```
$ ansible-playbook -i ~/playbooks/inventory httpd.yml
```

- Verify the service have been installed on the target application server
```
$ ansible stapp02 -i ~/playbooks/inventory -m shell -a 'systemctl status httpd; systemctl status php'
```

- Verify the DocumentRoot has been correctly updated
```
$ ansible stapp02 -m shell -a 'grep DocumentRoot /etc/httpd/conf/httpd.conf' -i ~/playbooks/inventory
```

- Verify the php file has been copied with the correct ownership, name and content
```
$ ansible stapp02 -m shell -a 'ls -l /var/www/html/myroot; cat /var/www/html/myroot/phpinfo.php' -i ~/playbooks/inventory
```