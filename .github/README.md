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
       - name: "Configure sudo settings, auth, and shell"
         ansible.builtin.include_role:
           name: ans_role_config_sudo
         vars:
           ask_password_timeout: 45
           password_prompt_timeout_minutes: 0
           use_root_umask: true
           set_auth_for_group: "wheel"
   ```

## Role Options

See the role `defaults` file, for overridable vars:

  * [defaults/main.yml](../defaults/main.yml)

Define these _optional_ vars for the role:

  * `set_auth_for_group`: [boolean] a group to grant full sudo authorization to
    (_NOTE_: mutually exclusive with `set_auth_for_user`)
  * `set_auth_for_user`: [boolean] a user to grant full sudo authorization to
    (_NOTE_: mutually exclusive with `set_auth_for_group`)
  * `enable_sudo_auth`: [boolean] if 'false', will disable all sudo auth for the
    user/group (defaults to 'true')
  * `auth_cmd_list`: [list] for group-auth or user-auth, authorize only a list
    of cmds
  * `req_sudo_password`: [boolean] require sudo password for group/user
    (defaults to 'true')
  * `ask_password_timeout`: [int] number of minutes sudo will wait between
    passwd asks
  * `password_prompt_timeout_minutes`: [int] on ask, timeout and abort after X
    minutes (0 for never)
  * `use_root_umask`: [boolean] make sudo use root-user umask (not user's) for
    file create

## Contributing

* Feel free to report a bug or propose a feature by opening a new
  [Issue](https://github.com/digimokan/ans_role_config_sudo/issues).
* Follow the project's [Contributing](CONTRIBUTING.md) guidelines.
* Respect the project's [Code Of Conduct](CODE_OF_CONDUCT.md).

