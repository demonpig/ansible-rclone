# Ansible Role: Rclone

Installs Rclone on various operating systems (RHEL/Centos, Debian/Ubuntu, FreeBSD, MacOS, Windows). Basically any operating system that is supported by both Ansible and Rclone, this role will work on.

## Role Variables
```yaml
rclone_version: v1.57.0
```
The version of rclone to install on the system.

## Dependencies
None

## Example Playbook
```yaml
---

- name: Example playbook
  hosts: all
  roles:
    - role: demonpig.rclone
```

## License
MIT
