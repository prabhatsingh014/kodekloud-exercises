- Create index.yml file at the location /home/thor/playbooks with the following content
```
$ vi /home/thor/playbooks/index.yml
---
- hosts: all
  become: yes
  gather_facts: yes
  tasks:
  - name: Create file using blockinfile module
    blockinfile:
      block: "Ansible managed node IP is {{ ansible_default_ipv4.address }}"
      create: yes
      path: /root/facts.txt

  - name: Install httpd server
    yum:
      name: httpd
      state: present

  - name: Copy facts.txt to app servers
    copy:
      src: /root/facts.txt
      dest: /var/www/html/index.html
      remote_src: yes

  - name: Start httpd server
    systemd:
      name: httpd
      state: started
      enabled: yes
```
- Save and exit the file

- Execute the ansible playbook to implement the changes
```
$ ansible-playbook -i inventory index.yml 
```
- Verify if the index.html has been created and httpd service is running on all app servers
```
$ ansible -m shell -a 'cat /var/www/html/index.html' -i inventory all
$ ansible -m shell -a 'systemctl status httpd' -i inventory all
```