Ansible Role: chezmoi
=========

An ansible role role that installs and initializes [chezmoi](https://github.com/twpayne/chezmoi).
In addition to the main application, the module creates a systemd service and timer to be used to setup auto updates of dotfiles for the users.

Requirements
------------

`git` should be installed before.

Role Variables
--------------

Available variables and their defaults values are listed in [defaults/main.yml](defaults/main.yml).

```yaml
chezmoi_repo: twpayne/chezmoi
chezmoi_version: latest
```
The repository and the version of `chezmoi` that will be installed.

```yaml
chezmoi_users: []
# chezmoi_users:
#   - user: XXX
#     repo: YYY [optional: dotfiles repository]
#     start_timer: bool [optional, default 'false']
```
The list of the local users and their dotfiles repositories. For each user in the list, if not already initialized, will be executed:
```sh
chezmoi init --apply <REPO>
```

`start_timer` controls wheter the systemd timer to keep the downloaded dotfiles repo in sync will be started and enabled for each user.

```yaml
chezmoi_update_cron: hourly
```
Set the `OnCalendar` parameter for the systemd timer unit. This value is the same for all the users.

Dependencies
------------

None.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yaml
- hosts: all
  vars:
    chezmoi_users:
    - user: my_user
      repo: my_dotfile_repo
      start_timer: true
  roles:
  - alecunsolo.chezmoi
```
License
-------

MIT

Notes
-----

Testing with molecule (including the docker images used) is ~~stolen from~~ heavily inspired by [Jeff Geerling](https://www.jeffgeerling.com/). Watch [his video](https://youtu.be/FaXVZ60o8L8) (and the other ones as well).
