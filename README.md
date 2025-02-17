# RHEL 8 CVE-2023-48795 Workaround

This Ansible role applies the workaround for **CVE-2023-48795** on **RHEL 8** systems. The vulnerability pertains to certain cryptographic policies related to OpenSSH and SSH configuration. This role helps mitigate the issue by adjusting specific cryptographic settings to disable the vulnerable cipher suites and enhance SSH security on affected systems.

This role is essential for RHEL 8 systems running OpenSSH and affected by **CVE-2023-48795**, which is a security flaw related to SSH encryption methods that could potentially expose systems to cryptographic weaknesses.

## Requirements

- **RHEL 8** or any compatible systems that support RHEL 8 policies.
- **OpenSSH** installed and running on the system.
- This role is designed for systems where SSH is actively used for remote management.

## Role Variables

Currently, there are **no configurable variables** for this role. All actions performed by the role are based on the CVE patch requirements, which involve creating specific configuration files, running crypto-policy updates, and restarting the SSH service.

## Files Created/Modified

The role performs the following actions:
- Creates a file under `/etc/crypto-policies/policies/modules/` to disable the vulnerable cipher (`CHACHA20-POLY1305`).
- Modifies OpenSSH configurations to ensure secure cryptographic protocols are in place.
- Applies changes to crypto-policies and restarts the SSH service to enforce the new configuration.
- Verifies that the unwanted ciphers and settings are removed from the SSH configurations.

## Example Playbook

To use this role, create a playbook that applies it to the target hosts:

```yaml
---
- name: Apply CVE-2023-48795 workaround to RHEL 8 systems
  hosts: all
  become: yes
  roles:
    - rhel8_cve_2023_48795
```

### Usage

- The role must be run with **root privileges** (`become: yes`) to ensure it can modify system-level configurations and restart the SSH service.
- The role will automatically apply the workaround by modifying system files and policies according to the CVE mitigation steps.
- It ensures that no residual vulnerable ciphers are left in the OpenSSH configuration.

## Supported Platforms

This role is designed for **RHEL 8** systems, but it should work on any compatible Linux distribution that follows similar cryptographic policies and has OpenSSH installed.

### Testing the Role

You can test whether the role has been successfully applied by verifying the changes in the SSH configuration files:

```bash
cat /etc/crypto-policies/back-ends/openssh.config
cat /etc/crypto-policies/back-ends/opensshserver.config
```

Ensure that the following settings are applied:
- The cipher `CHACHA20-POLY1305` is **disabled**.
- `ssh_etm = 0` should **not appear** in the configurations.

## License

This role is licensed under the **MIT License**.

---
