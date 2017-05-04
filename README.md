# UCLALib Ansible Role: Tomcat Web Service App Deployment

Ansible role to deploy Tomcat war files into pre-existing Tomcat installations.

## Dependencies

* A functioning tomcat environment created using `uclalib_role_tomcat`, or a tomcat environment that uses the same conventions for application naming and filesystem layout.

* A SFTP site containing the .war file to be deployed. The Ansible user's ssh public key must be installed in this SFTP account.

## Role Variables

Below is a list of variables available to the role. For defaults, reference `defaults/main.yml`

* `webapp_name` - Name of the tomcat webapp to be deployed into tomcat. This variable has no default value. It must be set for each run of this role using the `-e` flag for the `ansible-playbook` command.

* `sftp_server_name` - FQDN of the SFTP server where the .war file exists.

* `sftp_username` - Username of an account for connecting to the SFTP server.

* `sftp_path` - Path to the directory on the SFTP site containing the .war file.

* `ansible_ident_file` - Path to the Ansible SSH identity file for connecting to the SFTP site.

## Example Playbook
```
---

- name: uclalib_tomwebappdeploy.yml
  become: yes
  become_method: sudo
  hosts: test

  roles:
    - { role: uclalib_role_webservices }
```

## Example Usage

To execute this role, the following is an example usage of the `ansible-playbook` command.

Take note of the `-e` flag which is required to set the `webapp_name` variable.
```
ansible-playbook -i /etc/ansible/inventory.ini -l tomcatsrv.library.ucla.edu plays/uclalib_tomwebappdeploy.yml -e "webapp_name=app1" -v
```
