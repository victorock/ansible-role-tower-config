Ansible Tower Setup
=========

Simple Role to Setup Ansible Tower by Red Hat.

Requirements
------------

None

Role Variables
--------------

defaults/main.yml

```
---

organization: "VUIT"
organization_state: present
organization_description: "Organisation description "
verify_ssl: False

tower_team:
    name: "ExampleTeam1"
    description: "This is the best team in the world"
    organization: "{{ organization }}"
    state: present
    tower_users:
       - username: kjelleman
        # password: password
        # email: jdoe@example.org
        # first_name: John
        # last_name: Doe
        # superuser: false
        # state: present
       - username: kjelleman2
               # password: password
               # email: jdoe@example.org
               # first_name: John
               # last_name: Doe
               # superuser: false
               # state: present
       - username: jtoe
        # password: password
        # email: jtoe@example.org
        # first_name: Jane
        # last_name: Toe
        # superuser: true
        # state: present
    tower_projects:
        - name: "Team1_playbooks"
          description: "The playbooks for team 1 scm "
          organization: "{{ organization }}"
          scm_type: git
          scm_branch: "master"
          scm_update_on_launch: true
          scm_url: "https://github.com/example/team/Playbooks.git"
          state: present
    tower_inventories:
        - name: "Linux servers example"
          description: "Team1 Linux Servers"
          organization:  "{{ organization }}"
          state: present
          tower_hosts:
              - name: Server1
                description: "Server1 "
                state: present
              - name: Server2
                description: "Server2 "
                state: present
        - name: "Linux servers example2"
          description: "Team1 Linux Servers"
          organization:  "{{ organization }}"
          state: present
          tower_hosts:
              - name: Server1
                description: "Server3"
                state: present
              - name: Server2
                description: "Server4"
                state: present
    tower_credentials:
        - tower_credential:
             name: "foo_scm_credential"
             organization: "{{ organization }}"
             kind: "scm"
             description: This is a git credential for project Foo
             user: extktd
             state: present

```

Dependencies
------------

The following dependencies are defined in `meta/main.yml`:

- role: geerlingguy.repo-epel
  when: ansible_os_family == 'RedHat'
- role: geerlingguy.ansible

Example Playbook
----------------

```YAML
- name: "Setup Ansible Tower by Red Hat"
  hosts: tower
  become: true

  roles:
    - victorock.ansible-tower-setup
```

License
-------

GPLv3

Author Information
------------------

Victor da Costa
