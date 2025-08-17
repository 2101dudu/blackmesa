# Houses secrets that serve a generic purpose.

Create a folder for the group
```bash
mkdir <group> && cd <group>
```

For ease of use, create a file with the password:
```bash
echo "my_vault_password" > .ansible_vault_pass.txt
chmod 600 .ansible_vault_pass.txt
```

Create the vars file (with the name `vars.yml`):
```bash
touch vars.yml
```

Create the vault file (with the name `vault.yml`) - the structure of this file is the same as the vars file, but the variables' names must preced a `vault_` keyword:
```bash
ansible-vault create --vault-id <vault-id>@.ansible_vault_pass.txt vault.yml
```

And update `ansible.cfg` with the following line:
```
vault_identity_list=<vault-id>@group_vars/<group>/.ansible_vault_pass.txt
```

### Contains:
    - promox required fields for a minimal VM setup
