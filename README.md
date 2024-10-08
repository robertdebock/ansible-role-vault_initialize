# [Ansible role vault_initialize](#vault_initialize)

Initialize and unseal HashiCorp Vault.

|GitHub|GitLab|Downloads|Version|
|------|------|---------|-------|
|[![github](https://github.com/robertdebock/ansible-role-vault_initialize/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-vault_initialize/actions)|[![gitlab](https://gitlab.com/robertdebock-iac/ansible-role-vault_initialize/badges/master/pipeline.svg)](https://gitlab.com/robertdebock-iac/ansible-role-vault_initialize)|[![downloads](https://img.shields.io/ansible/role/d/robertdebock/vault_initialize)](https://galaxy.ansible.com/robertdebock/vault_initialize)|[![Version](https://img.shields.io/github/release/robertdebock/ansible-role-vault_initialize.svg)](https://github.com/robertdebock/ansible-role-vault_initialize/releases/)|

## [Example Playbook](#example-playbook)

This example is taken from [`molecule/default/converge.yml`](https://github.com/robertdebock/ansible-role-vault_initialize/blob/master/molecule/default/converge.yml) and is tested on each push, pull request and release.

```yaml
---
- name: Converge
  hosts: all
  become: true
  gather_facts: true

  roles:
    - role: robertdebock.vault_initialize
      vault_tls_skip_verify: true
```

The machine needs to be prepared. In CI this is done using [`molecule/default/prepare.yml`](https://github.com/robertdebock/ansible-role-vault_initialize/blob/master/molecule/default/prepare.yml):

```yaml
---
- name: Prepare
  hosts: all
  become: true
  gather_facts: false

  roles:
    - role: robertdebock.bootstrap
    - role: robertdebock.core_dependencies
    - role: robertdebock.hashicorp
    - role: robertdebock.vault
      vault_hardening_disable_swap: false
    - role: robertdebock.vault_configuration
      vault_configuration_listener_tcp:
        address: "127.0.0.1:8200"
        cluster_address: "127.0.0.1:8201"
        tls_disable: true
      vault_configuration_storage_raft:
        path: "/opt/vault/data"
        node_id: "{{ ansible_hostname }}"
```

Also see a [full explanation and example](https://robertdebock.nl/how-to-use-these-roles.html) on how to use these roles.

## [Role Variables](#role-variables)

The default values for the variables are set in [`defaults/main.yml`](https://github.com/robertdebock/ansible-role-vault_initialize/blob/master/defaults/main.yml):

```yaml
---
# defaults file for vault_initialize

# The address where Vault can be found, similar to `VAULT_ADDR`.
vault_initialize_addr: "https://localhost:8200"

# When Vault is installed using untrusted certificates, you can disable the verification of the certificates.
vault_tls_skip_verify: false

# You can show the (sensitive) information when initializing Vault. This includes the root token and unseal keys.
vault_initialize_show_information: true
```

## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/robertdebock/ansible-role-vault_initialize/blob/master/requirements.txt).

## [State of used roles](#state-of-used-roles)

The following roles are used to prepare a system. You can prepare your system in another way.

| Requirement | GitHub | GitLab |
|-------------|--------|--------|
|[robertdebock.bootstrap](https://galaxy.ansible.com/robertdebock/bootstrap)|[![Build Status GitHub](https://github.com/robertdebock/ansible-role-bootstrap/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-bootstrap/actions)|[![Build Status GitLab](https://gitlab.com/robertdebock-iac/ansible-role-bootstrap/badges/master/pipeline.svg)](https://gitlab.com/robertdebock-iac/ansible-role-bootstrap)|
|[robertdebock.bootstrap](https://galaxy.ansible.com/robertdebock/bootstrap)|[![Build Status GitHub](https://github.com/robertdebock/ansible-role-bootstrap/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-bootstrap/actions)|[![Build Status GitLab](https://gitlab.com/robertdebock-iac/ansible-role-bootstrap/badges/master/pipeline.svg)](https://gitlab.com/robertdebock-iac/ansible-role-bootstrap)|
|[robertdebock.core_dependencies](https://galaxy.ansible.com/robertdebock/core_dependencies)|[![Build Status GitHub](https://github.com/robertdebock/ansible-role-core_dependencies/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-core_dependencies/actions)|[![Build Status GitLab](https://gitlab.com/robertdebock-iac/ansible-role-core_dependencies/badges/master/pipeline.svg)](https://gitlab.com/robertdebock-iac/ansible-role-core_dependencies)|
|[robertdebock.hashicorp](https://galaxy.ansible.com/robertdebock/hashicorp)|[![Build Status GitHub](https://github.com/robertdebock/ansible-role-hashicorp/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-hashicorp/actions)|[![Build Status GitLab](https://gitlab.com/robertdebock-iac/ansible-role-hashicorp/badges/master/pipeline.svg)](https://gitlab.com/robertdebock-iac/ansible-role-hashicorp)|
|[robertdebock.vault](https://galaxy.ansible.com/robertdebock/vault)|[![Build Status GitHub](https://github.com/robertdebock/ansible-role-vault/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-vault/actions)|[![Build Status GitLab](https://gitlab.com/robertdebock-iac/ansible-role-vault/badges/master/pipeline.svg)](https://gitlab.com/robertdebock-iac/ansible-role-vault)|
|[robertdebock.vault_configuration](https://galaxy.ansible.com/robertdebock/vault_configuration)|[![Build Status GitHub](https://github.com/robertdebock/ansible-role-vault_configuration/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-vault_configuration/actions)|[![Build Status GitLab](https://gitlab.com/robertdebock-iac/ansible-role-vault_configuration/badges/master/pipeline.svg)](https://gitlab.com/robertdebock-iac/ansible-role-vault_configuration)|

## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/ansible-role-vault_initialize/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/robertdebock):

|container|tags|
|---------|----|
|[Amazon](https://hub.docker.com/r/robertdebock/amazonlinux)|Candidate|
|[Debian](https://hub.docker.com/r/robertdebock/debian)|all|
|[EL](https://hub.docker.com/r/robertdebock/enterpriselinux)|9|
|[Fedora](https://hub.docker.com/r/robertdebock/fedora)|39, 40|
|[Ubuntu](https://hub.docker.com/r/robertdebock/ubuntu)|all|

The minimum version of Ansible required is 2.12, tests have been done to:

- The previous version.
- The current version.
- The development version.

If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-vault_initialize/issues).

## [License](#license)

[Apache-2.0](https://github.com/robertdebock/ansible-role-vault_initialize/blob/master/LICENSE).

## [Author Information](#author-information)

[robertdebock](https://robertdebock.nl/)

Please consider [sponsoring me](https://github.com/sponsors/robertdebock).
