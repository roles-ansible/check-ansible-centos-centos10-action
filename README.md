[![Github Marketplace](https://raw.githubusercontent.com/roles-ansible/check-ansible-centos-centos10-action/main/.github/marketplace.svg?sanitize=true)](https://github.com/marketplace/actions/check-ansible-centos-centos10)
[![MIT License](https://raw.githubusercontent.com/roles-ansible/check-ansible-centos-centos10-action/main/.github/license.svg?sanitize=true)](https://github.com/roles-ansible/check-ansible-centos-centos10-action/blob/main/LICENSE)

Check Ansible CentOS 10 Stream
==============================
This action allows you to test your ansible role or your playbook in a Docker Container with ``quay.io/centos/centos:stream10``.

## Usage
To use the action simply create an ``ansible-centos-centos10.yml`` *(or choose custom ``*.yml`` name)* in the ``.github/workflows/`` directory.

For example:

```yaml
---
name: Ansible check centos:stream10  # feel free to pick your own name

# yamllint disable-line rule:truthy
on: [push, pull_request]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      # Important: This sets up your GITHUB_WORKSPACE environment variable
      - name: checkout git repo
        uses: actions/checkout@v3

      - name: ansible check with quay.io/centos/centos:stream10
        # optionally replace "main" with any valid git ref
        uses: roles-ansible/check-ansible-centos-centos10-action@main
        with:
          targets: "./"
          #  [required]
          #   Paths to your ansible role or playboox.yml you want to test
          #   Some Examples:
          #   targets: "role/my_role/"
          #   targets: "site.yml"
          #
          # group: ""
          #  [optional]
          #   When testing playbooks you have to tell ansible
          #   the group you that we write in our hosts file.
          #   example:
          #   group: 'servers'
          #
          # hosts: ""
          #  [optional]
          #   When testing playbooks you have to give one example
          #   host this action should use to test your playbook.
          #   > We only spawn one docker container that mean
          #   > we can only test one host at the time. Sorry
          #   some examples:
          #   hosts: 'localhost'
          #   hosts: 'srv01.example.com'
          #
          # requirements: ""
          #  [optional]
          #   When testing playbooks and you are using ansible galaxy,
          #   you may be interested in installing your requirements
          #   from ansible galaxy.
          #   To do this please provide us either the role name directly
          #   requirements: 'do1jlr.ansible_version'
          #   or your requiements.yml file.
          #   requirements: 'requirements.yml'
          #
          # tags: ""
          #  [optional]
          #   If you want to limit the test to some tags, you can use this
          #   tags or the skiptags option. It will trigger the --tags $tags
          #   option to ansible.
          #
          # skiptags: ""
          # [optional]
          #  See tags. This will trigger the --skip-tags $skiptags option
          #  to ansible.
```

Alternatively, you can run the ansible check only on certain branches:

```yaml

on:
  push:
    branches:
    - stable
    - release/v*
```

or on various [events](https://help.github.com/en/articles/events-that-trigger-workflows)

<br/>

 Contributing
-------------
If you are missing a feature or see a bug. Please report it. Or - if you like - open a pull-request.

 License
----------
The Dockerfile and associated scripts and documentation in this project are released under the [MIT License](LICENSE).

 Credits
--------------
+ The initial GitHub action has been created by [Stefan Stölzle](https://github.com/stoe) at
[stoe/actions](https://github.com/stoe/actions).
+ It was used by ansible for lint checks at [ansible/ansible-lint-action](https://github.com/ansible/ansible-lint-action.git)
+ It was modified from [L3D](https://github.com/do1jlr) to check ansible roles.
+ It was modified by [Jakuje](https://github.com/Jakuje/) for Centos 10 Stream.
