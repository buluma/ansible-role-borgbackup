# Ansible role [borgbackup](https://galaxy.ansible.com/ui/standalone/roles/buluma/borgbackup/documentation)

Set up backup to remote machine using Borg and Borgmatic.

|GitHub|Version|Issues|Pull Requests|Downloads|
|------|-------|------|-------------|---------|
|[![github](https://github.com/buluma/ansible-role-borgbackup/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-borgbackup/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-borgbackup.svg)](https://github.com/buluma/ansible-role-borgbackup/releases/)|[![Issues](https://img.shields.io/github/issues/buluma/ansible-role-borgbackup.svg)](https://github.com/buluma/ansible-role-borgbackup/issues/)|[![PullRequests](https://img.shields.io/github/issues-pr-closed-raw/buluma/ansible-role-borgbackup.svg)](https://github.com/buluma/ansible-role-borgbackup/pulls/)|[![Ansible Role](https://img.shields.io/ansible/role/d/buluma/borgbackup)](https://galaxy.ansible.com/ui/standalone/roles/buluma/borgbackup/documentation)|

## [Example Playbook](#example-playbook)

This example is taken from [`molecule/default/converge.yml`](https://github.com/buluma/ansible-role-borgbackup/blob/master/molecule/default/converge.yml) and is tested on each push, pull request and release.

```yaml
---
- name: Converge
  hosts: all

  roles:
    - role: buluma.borgbackup
      borg_encryption_passphrase: CHANGEME
      borg_repository: m5vz9gp4@m5vz9gp4.repo.borgbase.com:repo
      borg_source_directories:
        - /srv/www
        - /var/lib/automysqlbackup
      borg_exclude_patterns:
        - /srv/www/old-sites
      borg_retention_policy:
        keep_hourly: 3
        keep_daily: 7
        keep_weekly: 4
        keep_monthly: 6
      borgmatic_hooks:
        before_backup:
          - echo "`date` - Starting backup."
        postgresql_databases:
          - name: users
            hostname: database1.example.org
            port: 5433
```

The machine needs to be prepared. In CI this is done using [`molecule/default/prepare.yml`](https://github.com/buluma/ansible-role-borgbackup/blob/master/molecule/default/prepare.yml):

```yaml
---
- name: Prepare
  hosts: all
  become: no
  gather_facts: yes

  roles:
    - role: buluma.bootstrap

  pre_tasks:
    - name: Set ssh server package name for non-Archlinux ansible_os_family
      ansible.builtin.set_fact:
        openssh_package: "openssh-server"
      when: ansible_os_family != "Archlinux"

    - name: Set ssh server package name for Archlinux ansible_os_family
      ansible.builtin.set_fact:
        openssh_package: "openssh"
      when: ansible_os_family == "Archlinux"

    - name: Install openssh
      ansible.builtin.package:
        name: "{{ openssh_package }}"
        state: present
```

Also see a [full explanation and example](https://buluma.github.io/how-to-use-these-roles.html) on how to use these roles.

## [Role Variables](#role-variables)

The default values for the variables are set in [`defaults/main.yml`](https://github.com/buluma/ansible-role-borgbackup/blob/master/defaults/main.yml):

```yaml
---
# defaults file for borgbackup
borg_encryption_passphrase: ''
borg_exclude_patterns: []
borgmatic_config_name: config.yaml
borgmatic_large_repo: true
borgmatic_hooks:
  on_error:
    - echo "`date` - Error while creating a backup."
  before_backup:
    - echo "`date` - Starting backup."
  after_backup:
    - echo "`date` - Finished backup."
borgmatic_checks:
  - repository
borgmatic_check_last: 3
borgmatic_store_atime: true
borgmatic_store_ctime: true
borgmatic_relocated_repo_access_is_ok: false
borg_one_file_system: true
borg_exclude_from: []
borg_encryption_passcommand: false
borg_lock_wait_time: 5
borg_ssh_command: false
borg_remote_path: false
borg_remote_rate_limit: 0
borg_retention_policy:
  keep_hourly: 3
  keep_daily: 7
  keep_weekly: 4
  keep_monthly: 6
ssh_key_file: .ssh/id_ed25519
borgmatic_cron_name: borgmatic
borgmatic_cron_hour: "{{ 6 | random(seed=inventory_hostname) }}"
borgmatic_cron_minute: "{{ 59 | random(seed=inventory_hostname) }}"
borgmatic_cron_checks_day: "{{ range(1, 28) | random(seed=inventory_hostname) }}"
borgmatic_cron_checks_hour: "{{ range(9, 24) | random(seed=inventory_hostname) }}"
borgmatic_cron_checks_minute: "{{ 59 | random(seed=inventory_hostname) }}"
```

## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/buluma/ansible-role-borgbackup/blob/master/requirements.txt).

## [State of used roles](#state-of-used-roles)

The following roles are used to prepare a system. You can prepare your system in another way.

| Requirement | GitHub | Version |
|-------------|--------|--------|
|[buluma.bootstrap](https://galaxy.ansible.com/buluma/bootstrap)|[![Ansible Molecule](https://github.com/buluma/ansible-role-bootstrap/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-bootstrap/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-bootstrap.svg)](https://github.com/shadowwalker/ansible-role-bootstrap)|

## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://buluma.github.io/) for further information.

Here is an overview of related roles:

![dependencies](https://raw.githubusercontent.com/buluma/ansible-role-borgbackup/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/buluma):

|container|tags|
|---------|----|
|[Fedora](https://hub.docker.com/repository/docker/buluma/fedora/general)|all|
|[Debian](https://hub.docker.com/repository/docker/buluma/debian/general)|all|
|[Ubuntu](https://hub.docker.com/repository/docker/buluma/ubuntu/general)|focal, jammy|

The minimum version of Ansible required is 2.12, tests have been done to:

- The previous version.
- The current version.
- The development version.

If you find issues, please register them in [GitHub](https://github.com/buluma/ansible-role-borgbackup/issues)

## [Changelog](#changelog)

[Role History](https://github.com/buluma/ansible-role-borgbackup/blob/master/CHANGELOG.md)

## [License](#license)

[Apache-2.0](https://github.com/buluma/ansible-role-borgbackup/blob/master/LICENSE)

## [Author Information](#author-information)

[Shadow Walker](https://buluma.github.io/)

