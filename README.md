stuttgart-things/manage-proxmox-resources
=========================================

manage proxmox resources based on api calls (no binary is requiered by this role). 

### Role installation:
<details><summary><b>Install this role on your ansible host (click here)</b></summary>

```bash
cat <<EOF > /tmp/requirements.yaml
roles:
- src: https://github.com/stuttgart-things/manage-proxmox-resources.git
  scm: git
- src: https://github.com/stuttgart-things/create-send-webhook.git
  scm: git
EOF

ansible-galaxy install -r /tmp/requirements.yaml --force && ansible-galaxy collection install -r /tmp/requirements.yaml -f
```
</details>

## Example playbooks to use this role

<details><summary>Create VM pool (folder) (click here)</summary>

### Ansible command:
```bash
ansible-playbook /tmp/manage-proxmox-resources.yml
```

### Playbook: playbook.yml
```yaml
cat <<EOF > /tmp/manage-proxmox-resources.yaml
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
EOF
```
</details>

<details><summary>Delete VM (click here)</summary>

### Ansible command:
```bash
ansible-playbook /tmp/manage-proxmox-resources.yml
```

### Playbook: playbook.yml
```yaml
cat <<EOF > /tmp/manage-proxmox-resources.yml
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
EOF
```
</details>

<details><summary>Bulk Rename VM or VM template (click here)</summary>

### Ansible command:
```bash
ansible-playbook manage-proxmox-resources.yml
```

### Playbook: playbook.yml
```yaml
cat <<EOF > /tmp/manage-proxmox-resources.yml
---
- hosts: localhost
  vars:
    pve_cluster_url: "https://sthings-pve1.labul.sva.de:8006"
    pve_api_user:  "terraform@pve"
    pve_api_password: "secret"

    pve_bulk_rename_vms:
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
EOF
```
</details>

<details><summary>Single Rename VM or VM template (click here)</summary>

### Ansible command:
```bash
ansible-playbook playbook.yml
```

### Playbook: playbook.yml
```yaml
cat <<EOF > /tmp/manage-proxmox-resources.yml
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
EOF
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

## License
<details><summary>LICENSE</summary>

Copyright 2020 patrick hermann.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

</details>

Role history
----------------
| date  | who | changelog |
|---|---|---|
|2024-05-27  | Andre Ebert | Added Ansible-lint and Yamllint with skip rules and testing
|2020-10-13  | Marcel Zapf | Init

Author Information
------------------

```yaml
Andre Ebert (andre.ebert@sva.de); 05/2024

Marcel Zapf; 02/2022; Stuttgart-Things
```
