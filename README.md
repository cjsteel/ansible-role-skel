# Ansible Role: Skel

[![Build Status](https://travis-ci.org/AttestationLegale/ansible-role-skel.svg?branch=master)](https://travis-ci.org/AttestationLegale/ansible-role-skel) [![Ansible Galaxy](http://img.shields.io/badge/ansible--galaxy-skel-blue.svg)](https://galaxy.ansible.com/AttestationLegale/skel/)

Manage unix `skeleton`.

## Requirements

tNone

## Role Variables

For a complete list of variables, see `default/main.yml`.

    skel_default_owner: 'root'
    skel_default_group: 'root'
    skel_default_directory_mode: '0750'
    skel_default_file_mode: '0640'
    
    skel_default_link_force: False
    skel_default_link_mode: '0640'
    skel_default_link_state: 'link'
    
    skel_entries: []
    skel_group_entries: []
    skel_host_entries: []

## Dependencies

None

## Example Playbook

```yaml
---
  - hosts: all
    roles:
      - skel
    vars:
      skel_entries:
        - path: /etc/skel/.ssh
          state: directory
```

## Example as Dependancy

```yaml
---
# file: roles/display/meta/main.yml
dependencies:
  - role: ensure_dirs
    tags: ['minc', 'ensure_dirs']
    ensure_dirs_on_remote: '{{ display_ensure_dirs_on_remote }}'
    ensure_dirs_on_local : '{{ display_ensure_dirs_on_local }}'

  - role: skel
    become: true
    tags: ['minc', 'skel']
    skel_entries:

      - name: "meta/main.yml entry for /etc/skel/bin"
        path  : '/etc/skel/bin'
        user  : 'root'
        group : 'root'
        mode: '0755'
        state: 'directory' # options are 'directory' or 'absent'

      - name: 'template /etc/skel/bin/minc-toolkit-config.sh'
        src:  'minc-toolkit-config.sh'
        path: '/etc/skel/bin/minc-toolkit-config.sh'
        mode: '0755'
        state: 'template' # options are 'template' or 'absent'

      - name:  'template /etc/skel/bin/minc-toolkit-conf-{{ minc_ver}}.sh'
        src:   'versioned-minc-toolkit-config.sh'
        path:  '/etc/skel/bin/minc-toolkit-config-{{ minc_ver }}.sh'
        mode:  '0755'
        state: 'template' # options are 'template' or 'absent'

galaxy_info:
  author: your name
  description: your description
  company: your company (optional)
...
```
## Testing

### Vagrant

#### enable ansible env if using

```shell
source activate ansible
```

#### Create synced directory

```shell
mkdir -p .vagrant/synced
```

#### vagrant up

```shell
vagrant up
```

## License

MIT / BSD

## Author Information

This role was created in 2016 by [ALG](https://www.attestationlegale.fr)

This role was modified in 2017 by 