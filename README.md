# Incus Homelab

An Ansible playbook to setup some Incus containers and add them to your tailnet, useful for quick and dirty testing whilst protecting your "production" homelab.

### Pre-requisites
- [Incus](https://linuxcontainers.org/incus/)
- [Tailscale](https://tailscale.com/)

## Setup
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
## Create containers and add to tailnet
```shell
ansible-playbook playbook.yaml --vault-password-file .vaultkey
```

## Teardown containers
```shell
ansible-playbook teardown.yaml --vault-password-file .vaultkey
```
If you chose to make your key `ephemeral`, your containers will automatically be removed from your tailnet once the containrs disconnect (this may not happen immediatly), otherwise you will need to remove them from the [tailscale admin portal](https://login.tailscale.com/admin/machines).
