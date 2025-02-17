# RHEL 8 CVE-2023-48795 Workaround

This Ansible role applies the workaround for CVE-2023-48795 on RHEL 8 systems.

## Requirements

- RHEL 8 or compatible systems

## Role Variables

No configurable variables at the moment.

## Example Playbook

```yaml
---
- hosts: all
  become: yes
  roles:
    - rhel8_cve_2023_48795
