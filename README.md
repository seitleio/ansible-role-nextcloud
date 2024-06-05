Ansible Role: nextcloud
=========
[![Ansible Lint](https://github.com/seitleio/ansible-role-nextcloud/actions/workflows/ansible-lint.yaml/badge.svg)](https://github.com/seitleio/ansible-role-nextcloud/actions/workflows/ansible-lint.yaml)

This role creates a [Nextcloud](https://github.com/nextcloud/docker/tree/master) container and also an [OnlyOffice](https://github.com/ONLYOFFICE/Docker-CommunityServer) container.

Requirements
------------

As a prerequisite Python 3, Python Pip and Python docker module are required on the target host. You can install the packages manually or via ansible (see [Example Playbook](#example-playbook)).

```bash
# Manually install the packages with apt
apt install python3-full python3-pip python3-docker
```

Role Variables
--------------

| name                          | purpose                                               | default value                                     | note |
| ----------------------------- | ----------------------------------------------------- | ------------------------------------------------- | ---- |
| service_name                  | Used for the docker container name and the data path. | "nextcloud"                                       |      |
| service_data_location         | All data created by this service will be stored here. | "/data/services/{{ service_name }}"               |      |
| nextcloud_image               | Which docker image to use.                            | "nextcloud"                                       |      |
| nextcloud_image_version       | Which image version to use.                           | "29.0.0-apache"                                   |      |
| nextcloud_domain              | The public domain of the Nextcloud service.           | "nextcloud.example.com"                           |      |
| nextcloud_admin_username      |                                                       | "{{ lookup('env', 'NEXTCLOUD_ADMIN_USERNAME') }}" |      |
| nextcloud_admin_password      |                                                       | "{{ lookup('env', 'NEXTCLOUD_ADMIN_PASSWORD') }}" |      |
| nextcloud_mysql_db            |                                                       | "nextcloud"                                       |      |
| nextcloud_mysql_user          |                                                       | "nextcloud"                                       |      |
| nextcloud_mysql_password      |                                                       | ""                                                |      |
| nextcloud_mysql_root_password |                                                       | ""                                                |      |
| onlyoffice_jwt_secret         |                                                       | ""                                                |      |
| onlyoffice_domain             | The public domain of the OnlyOffice service.          | "onlyoffice.example.com"                          |      |

Dependencies
------------

* https://github.com/geerlingguy/ansible-role-docker

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yaml
- name: Run nextcloud on nextcloud_hosts
  hosts: nextcloud_hosts
  gather_facts: true
  tags:
    - setup_nextcloud
  pre_tasks:
  - name: Install requirements for Docker Ansible module
    ansible.builtin.apt:
      pkg:
      - python3-full
      - python3-pip
      - python3-docker
    when: ansible_distribution == 'Debian' or ansible_distribution == 'Ubuntu'
  roles:
    - role: ansible-role-nextcloud
```

License
-------
MIT

Author Information
------------------
Johannes Seitle <<johannes@seitle.io>>

<br/><br/><hr/>
<p align="center" style="font-size:24px">
<img src="https://avatars.githubusercontent.com/u/102231325?s=400&u=0c500c28b968020e0c306478e55779ed7a872a98&v=4" width="128"/><br/>
seitle.io
<p/>
