# IPTables Role for Ansible

An Ansible Role for configuring IPTables

## Variables

Here is an example variables file

```
---
iptables:
  rules:
    - { chain: FORWARD, in_interface: docker0, out_interface: eth0, jump: ACCEPT }
    - { chain: FORWARD, in_interface: eth0, out_interface: docker0, jump: ACCEPT }
```

This will create your custom rules in addition to essential rules show below:

```
- { chain: "INPUT", in_interface: "lo", jump: "ACCEPT" }
- { chain: "OUTPUT", out_interface: "lo", jump: "ACCEPT" }
- { chain: "OUTPUT", out_interface: "lo", jump: "ACCEPT" }
- { chain: "INPUT", match: "conntrack", ctstate: ["ESTABLISHED", "RELATED"], jump: "ACCEPT"}
- { chain: "OUTPUT", match: "conntrack", ctstate: ["ESTABLISHED"], jump: "ACCEPT"}
- { chain: "INPUT", match: "conntrack", ctstate: ["INVALID"], jump: "DROP"}
```

See the Ansible IPTables role for more examples: [https://docs.ansible.com/ansible/2.5/modules/iptables_module.html](https://docs.ansible.com/ansible/2.5/modules/iptables_module.html)

## Example Task with role

```
- name: install iptables
  hosts: all
  roles:
    - edr.iptables
```
