# ans-role-config-sudo

Ansible role to configure the system `sudo` utility.

[![Release](https://img.shields.io/github/release/digimokan/ans-role-config-sudo.svg?label=release)](https://github.com/digimokan/ans-role-config-sudo/releases/latest "Latest Release Notes")
[![License](https://img.shields.io/badge/license-MIT-blue.svg?label=license)](LICENSE.md "Project License")

## Table Of Contents

* [Purpose](#purpose)
* [Supported Operating Systems](#supported-operating-systems)
* [Quick Start](#quick-start)
    * [Load Role Via `ansible-galaxy` Command](#load-role-via-ansible-galaxy-command)
* [Role Options](#role-options)
* [Contributing](#contributing)

## Purpose

* Install `sudo`.
* Configure authorized `sudo` users, groups, ip-addresses, etc.

## Supported Operating Systems

* Arch Linux.

## Quick Start

### Load Role Via `ansible-galaxy` Command

1. Create `requirements.yml` in ansible project root, and add this content:

   ```yaml
   # requirements.yml
   - src: https://github.com/digimokan/ans-role-config-sudo
     version: master
     name: config-sudo
   ```

2. From the project root directory, install/download the role:

   ```shell
   $ ansible-galaxy install --role-file requirements.yml --roles-path ./roles --force-with-deps
   ```

   * _NOTE:_ `--force-with-deps` _ensures subsequent calls download updates_

3. Include the role like any local role, from the project playbook:

   ```yaml
   # playbook.yml
   - hosts: localhost
     connection: local
     tasks:
       - name: "Install and configure sudo authorizations"
         include_role:
           name: config-sudo
         vars:
           set_full_root_authority: true
           sudo_users_group: "wheel"
           ask_password_timeout: 45
           password_prompt_timeout_minutes: 0
   ```

## Role Options

See the role `defaults` file, for overridable vars:

  * [defaults/main.yml](../defaults/main.yml)

Define these _optional_ vars for the role:

  * `sudo_users_group`: a group to grant full sudo authorization to
  * `set_full_root_authority`: bool, grant full authority to user 'root'
  * `ask_password_timeout`: number of minutes sudo will wait between passwd asks
  * `password_prompt_timeout_minutes`: on ask, timeout and abort after X minutes (0 for never)
  * `use_root_umask`: make sudo use root-user umask (not user's) for file create
  * `user_for_sudo_customization`: user-name, for user-specific shell/env enhancements

## Contributing

* Feel free to report a bug or propose a feature by opening a new
  [Issue](https://github.com/digimokan/ans-role-config-sudo/issues).
* Follow the project's [Contributing](CONTRIBUTING.md) guidelines.
* Respect the project's [Code Of Conduct](CODE_OF_CONDUCT.md).

