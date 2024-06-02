# number_cruncher
ansible role for system provisioning

## requirements

## variables
- fqdn_hostname: true
  - set fqdn_hostname to false to set the hostname as the hostname part only
- virtual_machines: list/string
  - used by virt-sysprep to determine kvm domains to clean

## dependencies
requires the following role(s):
- [boot_loader](https://github.com/chomatz/boot_loader)
- [remote_management](https://github.com/chomatz/remote_management)
- [system_information](https://github.com/chomatz/system_information)
- [time_synchronization](https://github.com/chomatz/time_synchronization)

## examples
```
- name: deploy baseline configuration
  ansible.builtin.include_role:
    name: number_cruncher
    tasks_from: baseline.yml
  vars:
    fqdn_hostname: false
```
```
- name: deploy desktop environment
  ansible.builtin.include_role:
    name: number_cruncher
    tasks_from: desktop.yml
```
```
---
- name: prepare virtual machine(s) for templating
  hosts: "{{ nodes }}"
  tasks:
    - name: template preparation
      ansible.builtin.include_role:
        name: number_cruncher
        tasks_from: kvm_template.yml
    - name: assemble list of virtual machines
      ansible.builtin.set_fact:
        virtual_machines: "{{ ansible_play_hosts }}"
      delegate_to: localhost
      delegate_facts: true
      run_once: true
- name: cleanup virtual machine(s) for templating
  hosts: "{{ hypervisor }}"
  tasks:
    - name: template cleanup
      ansible.builtin.include_role:
        name: number_cruncher
        tasks_from: virt-sysprep.yml
      vars:
        virtual_machines: "{{ hostvars['localhost']['virtual_machines'] }}"
...
```
