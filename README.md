Ansible Tower Config
=========

Simple Role to Configure Ansible Tower by Red Hat.

Requirements
------------

None

Role Variables
--------------

defaults/main.yml

```
---
tower_config:
  host: "tower.example.com"
  username: "admin"
  password: "toweradmin"
  verify_ssl: false

  setting:
    license:
      company_name: "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX"
      contact_email: "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX"
      contact_name: "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX"
      hostname: "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX"
      instance_count: XXXXXX
      license_date: XXXXXXX
      license_key: "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX"
      license_type: "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX"
      subscription_name: "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX"
      trial: XXXX
      eula_accepted: true

  organization:
    README:
      name: "README"
      description: "README"
      users:
        - name: "infraops"
          password: "infraops"
          email: "infraops@acme.com"
          first_name: "Infrastructure"
          last_name: "Operations"
          superuser: true
          auditor: false
        - name: "netops"
          password: "netops"
          email: "netops@acme.com"
          first_name: "Network"
          last_name: "Operations"
          superuser: false
          auditor: false
        - name: "devops"
          password: "devops"
          email: "devops@acme.com"
          first_name: "Developer"
          last_name: "Operations"
          superuser: false
          auditor: false
        - name: "sysops"
          password: "sysops"
          email: "sysops@acme.com"
          first_name: "System"
          last_name: "Operations"
          superuser: false
          auditor: false
        - name: "secops"
          password: "secops"
          email: "secops@acme.com"
          first_name: "Security"
          last_name: "Operations"
          superuser: false
          auditor: true
      teams:
        - name: "infraops"
          description: "Infrastructure Operations"
          members:
            - name: "netops"
            - name: "devops"
            - name: "sysops"
            - name: "secops"
        - name: "netops"
          description: "Network Operations"
          members:
            - name: "netops"
        - name: "devops"
          description: "Developer Operations"
          members:
            - name: "devops"
        - name: "sysops"
          description: "System Operations"
          members:
            - name: "sysops"
        - name: "secops"
          description: "Security Operations"
          members:
            - name: "secops"
      credentials:
        - name: "empty-scm"
          username: Null
          password: Null
          kind: "scm"
          description: "Empty credential"
        - name: "network-nxos-ssh"
          kind: "ssh"
          description: "Credential for nxos"
          username: vagrant
          password: vagrant
        - name: "network-nxos-net"
          kind: "net"
          description: "Credential for nxos"
          username: vagrant
          password: vagrant
        - name: "system-linux-ssh"
          kind: "ssh"
          description: "Credential for Linux"
          username: vagrant
          password: vagrant
        - name: "system-windows-ssh"
          kind: "ssh"
          description: "Credential for Windows"
          username: vagrant
          password: vagrant
      projects:
        - name: "Dev: netops:ansible-tower-example"
          description: "Dev: netops:ansible-tower-example"
          scm_credential: "empty-scm"
          scm_type: "git"
          scm_branch: "dev"
          scm_update_on_launch: true
          scm_url: "https://github.com/ansible/tower-example"
        - name: "Dev: devops:ansible-tower-example"
          description: "Dev: devops:ansible-tower-example"
          scm_credential: "empty-scm"
          scm_type: "git"
          scm_branch: "dev"
          scm_update_on_launch: true
          scm_url: "https://github.com/ansible/tower-example"
        - name: "Dev: sysops:ansible-tower-example"
          description: "Dev: sysops:ansible-tower-example"
          scm_credential: "empty-scm"
          scm_type: "git"
          scm_branch: "dev"
          scm_update_on_launch: true
          scm_url: "https://github.com/ansible/tower-example"
        - name: "Dev: secops:ansible-tower-example"
          description: "Dev: secops:ansible-tower-example"
          scm_credential: "empty-scm"
          scm_type: "git"
          scm_branch: "dev"
          scm_update_on_launch: true
          scm_url: "https://github.com/ansible/tower-example"
      inventories:
        - name: "infraops"
          description: "infraops"
        - name: "netops"
          description: "netops"
        - name: "sysops"
          description: "sysops"
        - name: "secops"
          description: "secops"
      job_templates:
        - name: "Dev: netops:helloworld"
          description: "Dev: netops:helloworld"
          project: "Dev: netops:ansible-tower-example"
          playbook: "helloworld.yml"
          inventory: "netops"
          forks: 50
          limit: "dev"
          machine_credential: "network-nxos-ssh"
          network_credential: "network-nxos-net"
        - name: "Dev: devops:helloworld"
          description: "Dev: devops:helloworld"
          project: "Dev: netops:ansible-tower-example"
          playbook: "helloworld.yml"
          inventory: "devops"
          forks: 50
          limit: "dev"
          machine_credential: "system-linux-ssh"
        - name: "Dev: sysops:helloworld"
          description: "Dev: sysops:helloworld"
          project: "Dev: sysops:ansible-tower-example"
          playbook: "helloworld.yml"
          inventory: "sysops"
          forks: 50
          limit: "dev"
          machine_credential: "system-windows-ssh"
        - name: "Dev: secops:helloworld"
          description: "Dev: secops:helloworld"
          project: "Dev: secops:ansible-tower-example"
          playbook: "helloworld.yml"
          inventory: "secops"
          forks: 50
          limit: "dev"
          machine_credential: "system-linux-ssh"
      permissions:
        - team: "infraops"
          role: "admin"
          target_team: "infraops"
        - team: "netops"
          role: "admin"
          target_team: "netops"
        - team: "sysops"
          role: "admin"
          target_team: "sysops"
        - team: "secops"
          role: "admin"
          target_team: "secops"
        - team: "secops"
          role: "admin"
          credential: "empty-scm"
        - team: "netops"
          role: "use"
          credential: "empty-scm"
        - team: "devops"
          role: "use"
          credential: "empty-scm"
        - team: "sysops"
          role: "use"
          credential: "empty-scm"
        - team: "secops"
          role: "admin"
          credential: "network-nxos-ssh"
        - team: "netops"
          role: "use"
          credential: "network-nxos-ssh"
        - team: "secops"
          role: "admin"
          credential: "network-nxos-net"
        - team: "netops"
          role: "use"
          credential: "network-nxos-net"
        - team: "secops"
          role: "admin"
          credential: "system-linux-ssh"
        - team: "sysops"
          role: "use"
          credential: "system-linux-ssh"
        - team: "devops"
          role: "use"
          credential: "system-linux-ssh"
        - team: "secops"
          role: "admin"
          credential: "system-windows-ssh"
        - team: "sysops"
          role: "use"
          credential: "system-windows-ssh"
        - team: "devops"
          role: "use"
          credential: "system-windows-ssh"
        - team: "netops"
          role: "admin"
          project: "Dev: netops:ansible-tower-example"
        - team: "devops"
          role: "admin"
          project: "Dev: devops:ansible-tower-example"
        - team: "secops"
          role: "admin"
          project: "Dev: secops:ansible-tower-example"
        - team: "sysops"
          role: "admin"
          project: "Dev: sysops:ansible-tower-example"
        - team: "netops"
          role: "admin"
          job_template: "Dev: netops:helloworld"
        - team: "devops"
          role: "admin"
          job_template: "Dev: devops:helloworld"
        - team: "sysops"
          role: "admin"
          job_template: "Dev: sysops:helloworld"
        - team: "secops"
          role: "admin"
          job_template: "Dev: secops:helloworld"
```

Dependencies
------------

The following dependencies are defined in `meta/main.yml`:

```YAML
dependencies:
  - role: geerlingguy.pip
    pip_install_packages:
      - name: ansible-tower-cli

```
Example Playbook
----------------

```YAML
- name: "Configure Ansible Tower by Red Hat"
  hosts: tower
  become: true

  roles:
    - victorock.tower_config
```

License
-------

GPLv3

Author Information
------------------

Victor da Costa
