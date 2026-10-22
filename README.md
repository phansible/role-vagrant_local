# Phansible Role: Vagrant Local

An Ansible Role that sets the hostname of a [Phansible](http://phansible.com/) Vagrant box and maps it to `127.0.0.1` in `/etc/hosts`.

## Requirements

- A Linux guest with the `hostname` command. The role has no platform metadata and no automated tests.
- Ansible (no minimum version declared)
- Root on the target: the tasks do not set `become`, so run the play with `become: yes`

## Role Variables

The role has no defaults. It reads one key from the `vagrant_local` dictionary that Phansible generates:

| Variable | Default | Description |
| --- | --- | --- |
| `vagrant_local.vm.hostname` | none, required | Hostname written to `/etc/hostname`, applied with `hostname`, and added to the `127.0.0.1` line in `/etc/hosts` |

The other keys Phansible puts under `vagrant_local.vm` (box, IP, memory, shared folder) are used by the generated Vagrantfile, not by this role.

The `/etc/hosts` task replaces the whole `127.0.0.1` line with `127.0.0.1 localhost <hostname>`. The two hostname tasks are shell commands, so they report a change on every run.

## Dependencies

None.

## Example Playbook

```yaml
- hosts: all
  become: yes
  vars:
    vagrant_local:
      vm:
        hostname: phansible
  roles:
    - vagrant_local
```

## License

This role is released under the terms of the license specified in the repository or if not specified, under the MIT license.

## Author Information

This role was created in 2014 by [The Phansible Team & Contributors](https://github.com/phansible/role-vagrant_local/graphs/contributors).
