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
echo <your-vault-password> >> .vaultkey
sudo chmod 600 .vaultkey
```
and finally:
```shell
ansible-playbook playbook.yaml --vault-password-file .vaultkey
```
