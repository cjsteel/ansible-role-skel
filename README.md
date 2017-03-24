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
# file: roles/shorewall/meta/main.yml
dependencies:
  - { role: skel, 
       skel_entries:
        - path: /etc/skel/.ssh,
          state: directory

        - type: 'blockinfile'    
          path: "/etc/skel/.bashrc"
          insertafter: "EOF"
          block: |
            # if running bash
            if [ -n "$BASH_VERSION" ]; then
                # include /opt/display/bin/display if it exists
                if [ -f "/opt/display/bin/display" ]; then
                    PATH="/opt/display/bin:$PATH"
                fi
            fi
          state: "present"
    }
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