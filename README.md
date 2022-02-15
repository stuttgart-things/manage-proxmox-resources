stuttgart-things/manage-proxmox-resources
=========================================

This Ansible role manage proxmox resources. This role is based on api calls, no other binary is requiered by this role. 

### Role installation:
<details><summary><b>Install this role on your ansible host (click here)</b></summary>

```
cat <<EOF > /tmp/requirements.yaml
roles:
- src: git@codehub.sva.de:Lab/stuttgart-things/supporting-roles/manage-proxmox-resources.git
  scm: git

EOF
ansible-galaxy install -r /tmp/requirements.yaml --force && ansible-galaxy collection install -r /tmp/requirements.yaml -f
```
</details>

For more information about stuttgart-things role installation visit: [Stuttgart-Things howto install role](https://codehub.sva.de/Lab/stuttgart-things/meta/documentation/doc-as-code/-/blob/master/howtos/howto-install-role.md)

## Example playbooks to use this role

<details><summary>Create VM pool (folder) (click here)</summary>

### Ansible command:
```
ansible-playbook playbook.yml
```

### Playbook: playbook.yml
```
---
- hosts: localhost
  vars:
    pve_cluster_url: "https://sthings-pve1.labul.sva.de:8006"
    pve_api_user:  "terraform@pve"
    pve_api_password: "secret"

    pve_pools :
      - name: pool1
      - name: pool2

  roles:
    - manage-proxmox-resources
```
</details>

<details><summary>Delete VM (click here)</summary>

### Ansible command:
```
ansible-playbook playbook.yml
```

### Playbook: playbook.yml
```
---
- hosts: localhost
  vars:
    pve_cluster_url: "https://sthings-pve1.labul.sva.de:8006"
    pve_api_user:  "terraform@pve"
    pve_api_password: "secret"

    pve_delete_vms:
      - name: badvm1
        node: sthings-pve1
      - name: badvm2
        node: sthings-pve1
      - name: badvm3
        node: sthings-pve1

  roles:
    - manage-proxmox-resources
```
</details>

<details><summary>Bulk Rename VM or VM template (click here)</summary>

### Ansible command:
```
ansible-playbook playbook.yml
```

### Playbook: playbook.yml
```
---
- hosts: localhost
  vars:
    pve_cluster_url: "https://sthings-pve1.labul.sva.de:8006"
    pve_api_user:  "terraform@pve"
    pve_api_password: "secret"

    pve_rename_vms:
      - current_vm_name: vm1
        expected_vm_name: myvm
        node: sthings-pve1
      - current_vm_name: vm2
        expected_vm_name: mygoodvm
        node: sthings-pve1
      - current_vm_name: vm3
        expected_vm_name: mybestvm
        node: sthings-pve1

  roles:
    - manage-proxmox-resources
```
</details>

<details><summary>Single Rename VM or VM template (click here)</summary>

### Ansible command:
```
ansible-playbook playbook.yml
```

### Playbook: playbook.yml
```
---
- hosts: localhost
  vars:
    pve_cluster_url: "https://sthings-pve1.labul.sva.de:8006"
    pve_api_user:  "terraform@pve"
    pve_api_password: "secret"
    pve_node: sthings-pve1

    pve_current_vm_name: vm1
    pve_expected_vm_name: myvm


  roles:
    - manage-proxmox-resources
```
</details>

## Requirements and Dependencies:
- Ubuntu 20.04
- Fedora 34
- CentOS 8
- CentOS 7

### Features:
- Create vm pool
- Remove vm
- Rename vm/template

## Version:
```
DATE            WHO            WHAT
2020-10-13      Marcel Zapf    Init
```

License
-------

BSD

Author Information
------------------

Marcel Zapf; 02/2022; SVA GmbH
