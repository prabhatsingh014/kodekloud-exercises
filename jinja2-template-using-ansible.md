- First part of the question is to update the playbook.yml file to update the hosts, tasks are supposed to run the asked host only.
- Update the ~/ansible/playbook.yml file with the hostname against the hosts: entry. Ensure that the hostname exist in the ~/ansible/inventory file as well.

# $ vi ~/ansible/playbook.yml
---
- hosts: stapp03
  become: yes
  become_user: root
  roles:
    - role/httpd
    
# Save and exit the file.

# Second part of the question is to create a jinja2 html template, which will then copied over to the target node and should refer only the target node on which it's supposed to run.
# Create a file index.html.j2 with the following content.

# $ vi /home/thor/ansible/role/httpd/templates/index.html.jinja2
<!DOCTYPE html>
<html lang="en">
<head>
</head>
<body>
    <h1>This file was created using Ansible on {{ inventory_hostname }}</h1>
</body>
</html>

# Save and exit the file.

# Third, fourth & maybe fifth parts of the question are to copy the template to the target node using ansible playbook with the respective hostname, having owner as the sudo user of the target and permission to be 0655.
# Edit the /home/thor/ansible/role/httpd/tasks/main.yml and add below task to accomplish

# $ vi /home/thor/ansible/role/httpd/tasks/main.yml

- name: Copy html file onto the target node
  template:
    src: index.html.j2
    dest: /var/www/html/index.html
    owner: banner
    group: banner
    mode: '0655'
    
# Save and exit the file.

# Last part of the question asks that the ansible-playbook command "ansible-playbook -i inventory playbook.yml" should run as it is without referencing any other variable or any other path.
# To accomplish this, /etc/ansible/ansible.cfg should be setup

# Edit /etc/ansible/ansible.cfg file with sudo user and modify the following entries

# $ vi /etc/ansible/ansible.cfg
inventory = /home/thor/ansible/inventory
roles_path = /etc/ansible/roles:/home/thor/ansible/role

# Save and exit the file.

# Run the following command from ansible directory.
# cd ~/ansible
# ansible-playbook -i inventory playbook.yml