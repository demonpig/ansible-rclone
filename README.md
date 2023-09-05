# demonpig.rclone

This role will install [rclone](https://github.com/rclone/rclone) onto a managed host.

### Requirements

- Playbook must gather facts about the managed host prior to executing the role's tasks. This is because the role utilizes the `ansible_distribution` fact variable when installing package dependencies.

### Role Variables

```yaml
rclone_version: latest
```

Specifies the version of the rclone to install on the managed host. The role pulls the artifacts from https://github.com/rclone/rclone/releases.

If the variable is set to `latest` (default), then the role will perform a check against the repository for the latest release.

### Dependencies

- Ansible 2.9+

### Example Playbook

```yaml
---

- name: Install Rclone
  hosts: all

  roles:
    - name: demonpig.rclone
```

### License

MIT
