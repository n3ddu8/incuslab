# Incus Homelab

Generate a [Tailscale Auth Key](https://login.tailscale.com/admin/settings/authkeys). Ensure to make the key `reusable`, for Incus containers that I spin up and tear down a lot, I also choose `ephemeral`. Run:
```shell
ansible-vault create group_vars/all/vault.yml
```
Populate it with:
```shell
tailscale_authkey: <your-key>
```
Now run:
```shell
ansible-playbook playbook.yaml -JK
```
where `-J` is shorthand for `--ask-vault-password` and `-K` is shorthand for `--ask-become-pass` and will prompt the user for their passwords at run-time.
