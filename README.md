Ansible role: aqua
==================

Install and configure aqua binary version manager.

Role Variables
--------------

```
ENTRY POINT: *main* - Install and configure aqua binary version manager

Options (= indicates it is required):

- aqua_arch_map  Mapping of the possible values of
                  ansible_facts.architecture to the aqua package
                  architectures
          default: null
          type: dict

- aqua_checksum_type  The aqua package checksum type
          default: sha256
          type: str

- aqua_github_checksum_filename  Filename for the aqua package
                                  checksums file on github
          default: checksums.txt
          type: str

- aqua_github_org  Name of organisation for aqua github repository
          default: aquaproj
          type: str

- aqua_github_repo  Name of aqua github repository
          default: aqua
          type: str

- aqua_github_token  Optional bearer token to use to authenticate
                      with api.github.com
          default: ''
          type: str

- aqua_global_install  If true, install binaries from global aqua
                        config file
          default: 'false'
          type: str

- aqua_global_install_args  Extra arguments to use when installing
                             binaries from global aqua config file
          default: --only-link
          type: str

- aqua_global_install_randomized_delay  Delay the aqua global install
                                         timer by a random time up to
                                         this value or empty string
                                         for no delay
          default: 6h
          type: str

- aqua_global_install_time  How often to install binaries from global
                             aqua config file, accepts a systemd time,
                             see
                             https://www.freedesktop.org/software/systemd/man/latest/systemd.time.html,
                             or "never"
          default: daily
          type: str

- aqua_install  If true, install aqua
          default: true
          type: bool

- aqua_update_randomized_delay  Delay the aqua update timer by a
                                 random time up to this value or empty
                                 string for no delay
          default: 6h
          type: str

- aqua_update_time  How often to update aqua, accepts a systemd time,
                     see
                     https://www.freedesktop.org/software/systemd/man/latest/systemd.time.html,
                     or "never"
          default: daily
          type: str

- aqua_users  List of user accounts to install aqua for
          default: []
          elements: dict
          type: list
          options:

          = username  Name of the user account
            type: str

- aqua_vacuum  If true, remove unused binaries from global aqua
                config file
          default: 'false'
          type: str

- aqua_vacuum_args  Extra arguments to use when removing unused
                     binaries from global aqua config file
          default: ''
          type: str

- aqua_vacuum_randomized_delay  Delay the aqua vacuum timer by a
                                 random time up to this value or empty
                                 string for no delay
          default: 6h
          type: str

- aqua_vacuum_time  How often to remove unused binaries from global
                     aqua config file, accepts a systemd time, see
                     https://www.freedesktop.org/software/systemd/man/latest/systemd.time.html,
                     or "never"
          default: daily
          type: str

- aqua_version  Version to install (use "latest" for the latest
                 version)
          default: latest
          type: str
```

Installation
------------

This role can either be installed manually with the ansible-galaxy CLI tool:

    ansible-galaxy install git+https://github.com/wandansible/aqua,main,wandansible.aqua

Or, by adding the following to `requirements.yml`:

    - name: wandansible.aqua
      src: https://github.com/wandansible/aqua

Roles listed in `requirements.yml` can be installed with the following ansible-galaxy command:

    ansible-galaxy install -r requirements.yml

Example Playbook
----------------

    - hosts: all
      roles:
         - role: wandansible.aqua
           become: true
           vars:
             aqua_users:
               - username: example
