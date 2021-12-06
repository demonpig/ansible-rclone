# Ansible Role: Rclone

Installs rclone on target system.

## Overview
This is a high-level overview how the role works:
1. Establish version of rclone to install by visiting rclone.org/version.txt
2. Construct download URL
3. Install dependencies
4. Create download folder in /var/tmp
5. Download and install rclone

## Role Variables
```yaml
rclone_version: current
```
The version of rclone to install on the system.

```yaml
rclone_url: ''
```
A URL to download a zip archive of rclone from. By default the role will use the `rclone_version` variable to construct the URL. This variable allows ansible to download from an internal site.

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

```yaml
---

- name: Example Playbook
  hosts: all
  roles:
    - role: demonpig.rclone
      rclone_version: beta
```

```yaml
---

- name: Example Playbook
  hosts: all
  roles:
    - role: demonpig.rclone
      rclone_url: 'https://internal-site.example.com/path/to/rclone.zip'
```

## License
MIT
