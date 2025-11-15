# ans_role_config_sudo

Ansible role to configure the system `sudo` utility.

[![Release](https://img.shields.io/github/release/digimokan/ans_role_config_sudo.svg?label=release)](https://github.com/digimokan/ans_role_config_sudo/releases/latest "Latest Release Notes")
[![License](https://img.shields.io/badge/license-MIT-blue.svg?label=license)](LICENSE.md "Project License")

## Table Of Contents

* [Purpose](#purpose)
* [Supported Operating Systems](#supported-operating-systems)
* [Quick Start](#quick-start)
    * [Use From Playbook](#use-from-playbook)
* [Role Options](#role-options)
* [Contributing](#contributing)

## Purpose

* Install `sudo`.
* Configure authorized `sudo` users, groups, etc.
* Configure general `sudo` command settings.

## Supported Operating Systems

* Arch Linux.
* FreeBSD.

## Quick Start

### Use From Playbook

1. Create `requirements.yml` in ansible project root, and add this content:

   ```yaml
   # requirements.yml
   - src: https://github.com/digimokan/ans_role_config_sudo
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
       - name: "Configure sudo settings and sudo permissions for users and groups"
         ansible.builtin.include_role:
           name: ans_role_config_sudo
         vars:
           cfg_sudo_ask_password_timeout: 45
           cfg_sudo_password_prompt_timeout_minutes: 0
           cfg_sudo_sudoers_rules:
             - label: "ansible_user2_all_auths"
               sudoer_name: "user2"
               # Note: either 'user' or 'group':
               sudoer_type: "user"
               allow_run_on_host: "ALL"
               allow_run_as_user: "ALL"
               # Note: may be list of commands as well:
               allow_commands: "ALL"
               req_passwd: true
   ```

## Role Options

Vars with default values, which can be overridden in the playbook:

  * [overridable](../defaults/main/overridable/)

Vars defined by this role, exported with `public: true`, for use in other roles:

  * [export vars](../defaults/main/export/main.yml)

## Contributing

* Feel free to report a bug or propose a feature by opening a new
  [Issue](https://github.com/digimokan/ans_role_config_sudo/issues).
* Follow the project's [Contributing](CONTRIBUTING.md) guidelines.
* Respect the project's [Code Of Conduct](CODE_OF_CONDUCT.md).

