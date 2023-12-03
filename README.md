I add `roles_path=./roles` to ansible.cfg and use something like the following:
```
- import_playbook: debian_playbooks/devsec_hardening.yml
  vars:
    os_harden: "{{ devsec_os_harden | default('false') }}"
    ssh_harden: "{{ devsec_ssh_harden | default('false') }}"

- import_playbook: debian_playbooks/base.yml
  vars:
    _base_role: "{{ base_role | default('true') }}"

- import_playbook: debian_playbooks/nftables.yml
  vars:
    _nftables_role: "{{ nftables_role | default('true') }}"

- import_playbook: debian_playbooks/wireguard.yml
  when: install_wireguard | default('false')

- import_playbook: debian_playbooks/update.yml
  when: update_host | default('true')
```
