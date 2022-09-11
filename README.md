# [borgbackup](#borgbackup)

Set up backup to remote machine using Borg and Borgmatic.

|GitHub|GitLab|Quality|Downloads|Version|Issues|Pull Requests|
|------|------|-------|---------|-------|------|-------------|
|[![github](https://github.com/buluma/ansible-role-borgbackup/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-borgbackup/actions)|[![gitlab](https://gitlab.com/buluma/ansible-role-borgbackup/badges/master/pipeline.svg)](https://gitlab.com/buluma/ansible-role-borgbackup)|[![quality](https://img.shields.io/ansible/quality/)](https://galaxy.ansible.com/buluma/borgbackup)|[![downloads](https://img.shields.io/ansible/role/d/)](https://galaxy.ansible.com/buluma/borgbackup)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-borgbackup.svg)](https://github.com/buluma/ansible-role-borgbackup/releases/)|[![Issues](https://img.shields.io/github/issues/buluma/ansible-role-borgbackup.svg)](https://github.com/buluma/ansible-role-borgbackup/issues/)|[![PullRequests](https://img.shields.io/github/issues-pr-closed-raw/buluma/ansible-role-borgbackup.svg)](https://github.com/buluma/ansible-role-borgbackup/pulls/)|

## [Example Playbook](#example-playbook)

This example is taken from `molecule/default/converge.yml` and is tested on each push, pull request and release.
```yaml
---
- name: Converge
  hosts: all
  tasks:
    - name: "Include buluma.borgbackup"
      include_role:
        name: "buluma.borgbackup"
```


## [Role Variables](#role-variables)

The default values for the variables are set in `defaults/main.yml`:
```yaml
---
# defaults file for borgbackup
```

## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/buluma/ansible-role-borgbackup/blob/main/requirements.txt).


## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://buluma.github.io/) for further information.

Here is an overview of related roles:

![dependencies](https://raw.githubusercontent.com/buluma/ansible-role-borgbackup/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/buluma):

|container|tags|
|---------|----|
|fedora|all|

The minimum version of Ansible required is 2.1, tests have been done to:

- The previous version.
- The current version.
- The development version.



If you find issues, please register them in [GitHub](https://github.com/buluma/ansible-role-borgbackup/issues)

## [Changelog](#changelog)

[Role History](https://github.com/buluma/ansible-role-borgbackup/blob/master/CHANGELOG.md)

## [License](#license)

Apache-2.0

## [Author Information](#author-information)

[buluma](https://buluma.github.io/)
