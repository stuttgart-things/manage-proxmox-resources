stuttgart-things/manage-proxmox-resources
=========================================

This Ansible role can manage proxmox resources via api calls. 

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
    api_user:  "terraform@pve"
    api_password: "secret"

    pve_pools :
      - name: testpool

  roles:
    - manage-proxmox-resources
```