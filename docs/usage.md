# Using demonpig.rclone role
This document will outline several different ways to use the `demonpig.rclone` role. It has been designed to be flexible as not all environments allow for complete access to the internet. 

### Normal Install
```
---

- name: Install rclone playbook
  hosts: all
  gather_facts: true
  roles:
    - name: demonpig.rclone
```

### Disconnected Environment
For this scenario, the managed host does not have access to Github or other sites on the internet. It will only have access to an internal S3-compatible object storage server and rclone is a required tool. The controller (host running the ansible playbook) will require access to the Github.

```
---

- name: Install rclone playbook
  hosts: all
  gather_facts: true

  vars:
    # Need to specify a specific version in order to prevent ansible from 
    # contacting the GitHub repo from the managed host where rclone will
    # be installed onto.
    rclone_version: v1.63.1

  tasks:
    - name: Create tmp download location on localhost
      register: tmp_download_dir
      ansible.builtin.tempfile:
        state: directory

    # this will download the rclone archive locally to a temp directory
    - name: Download rclone onto localhost
      delegate_to: localhost
      vars:
        rclone_download_path: "{{ tmp_download_dir.path }}"
      ansible.builtin.include_role:
        name: demonpig.rclone
        tasks_from: download

    - name: Create the tmp download location on managed host
      ansible.builtin.file:
        path: /var/tmp/ansible-role-rclone
        state: directory

    # this will sync all of the content of the temp directory to the 
    # managed host. Only the rclone archive should live in this dir.
    - name: Upload the local archive
      ansible.builtin.copy:
        src: "{{ tmp_download_dir.path }}/"
        dest: /var/tmp/ansible-role-rclone/

    - name: Install rclone
      ansible.builtin.include_role:
        name: demonpig.rclone
        tasks_from: install
```
