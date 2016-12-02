# UCLALib Ansible Role: Tomcat Web Service App Deployment
Ansible role to deploy Library Web Services tomcat webapps

# Dependencies

You have a functioning tomcat environment created using `uclalib_role_tomcat`.

You have a SFTP site containing the .war file to be deployed. The Ansible user's ssh public key must be installed in this SFTP account.

# Role Variables

Below is a list of variables available to the role. For defaults, reference `defaults/main.yml`

* Name of the tomcat webapp to be deployed into tomcat. This variable has no default value. It must be set for each run of this role using the `-e` flag for the `ansible-playbook` command.
```
webapp_name: app1
```
* FQDN of the SFTP server where the webapp .war file exists.
```
sftp_server_name: sftp.library.ucla.edu
```
* Username of an account for connecting to the SFTP server.
```
sftp_username: sftpuser
```
* Path to the directory on the SFTP site containing the .war file.
```
sftp_path: /build
```
* Path to the Ansible identity file for connecting to the SFTP site.
```
ansible_ident_file: /home/ansible/.ssh/id_rsa
```

# Example Playbook
```
---

- name: uclalib_tomwebappdeploy.yml
  become: yes
  become_method: sudo
  hosts: test

  roles:
    - { role: uclalib_role_webservices }
```

# Example Usage

To execute this role, the following is an example usage of the `ansible-playbook` command.

Take note of the `-e` flag which is required to set the `webapp_name` variable.
```
ansible-playbook -i /etc/ansible/inventory.ini -l tomcatsrv.library.ucla.edu plays/uclalib_tomwebappdeploy.yml -e "webapp_name=app1" -v
```
