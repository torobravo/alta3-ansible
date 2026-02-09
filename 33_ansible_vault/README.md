# Ansible Vault
To encode text files with Ansible Vault. Vault installs alongside Ansible, so you already have it on your system. Its job is to both encrypt text files (password files, variable files, playbooks), as well as decrypt. With ansible vault, you can permanently decrypt files, or just decrypt them for run-time. The default cipher is AES (which is shared-secret based).

Encrypt a file with ansible-vault
```bash
    ansible-vault encrypt ~/mycode/vars/mypasswords.yml
```

To edit an encrypted file in place, use the ansible-vault edit command. This command will decrypt the file to a temporary file and allow you to edit the file, saving it back when done and removing the temporary file:
```bash
    ansible-vault edit ~/mycode/vars/mypasswords.yml
```

Suppose typing out the password every single time you try to use this encrypted file isn't desirable. Let's put the password inside a hidden file instead.
```bash
    echo 'qwerty' > ~/mycode/.vaultpw
```

Now run the same command above, but by using the --vault-password-file option you won't have to type in the password yourself.
```bash
    ansible-vault edit ~/mycode/vars/mypasswords.yml --vault-password-file=~/mycode/.vaultpw
```

Now let's decrypt that file with ansible-vault.
```bash
    ansible-vault decrypt ~/mycode/vars/mypasswords.yml
```

## Encrypted playbook
Create a playbook.

**Encrypt** the playbook file with ansible-vault.
```bash
    ansible-vault encrypt ~/mycode/playbook-vault01.yml
```

To run the encrypted playbook:
```bash
    ansible-playbook --vault-id @prompt ~/mycode/playbook-vault01.yml
```

To run without needing to prompt for the paasword
```bash
    ansible-playbook ~/mycode/playbook-vault01.yml --vault-password-file=~/mycode/.vaultpw
```

## Encrypt a text file and use it inside a playbook
* Create a variable file
* Encrypt it with ansible-vault
* Create a playbook that uses the variable
* Execute the playbook with the following command
```bash
    ansible-playbook ~/mycode/playbook-vault02.yml -e @~/mycode/vars/oscreds.yml --vault-id @prompt
```

## Encrypt a password string and use it inside a playbook
Suppose we wanted to create a playbook with encrypted vars inside of it. Run the following command to encrypt the string `pAssw0rD` and map it to the key `mypass`. Note, if you were to use a $ in your password, be sure to ESCAPE it with a backslash, or it will be interpreted by the shell (passing $$ at the shell will echo a PID). Therefore, the proper way to pass a password containing $ symbols is `pA\$\$w0rD`
```bash
    ansible-vault encrypt_string "pAssw0rD" --name "mypass"
```

Now save it to a file
```bash
    ansible-vault encrypt_string "pAssw0rD" --name "mypass" > /home/student/mycode/vault_var.yml
```

Create a playbook that uses it
```yaml
---
- name: encrypt a string
  connection: local
  hosts: localhost
  gather_facts: no

  vars_files:
    - /home/student/mycode/vault_var.yml

  tasks:
    - name: print an encrypted string
      ansible.builtin.debug:
         msg: "{{ mypass }}"

```

Run the playbook with the following command
```bash
    ansible-playbook ~/mycode/playbook-vault03.yml --ask-vault-pass
```

## Run playbook with vault-id
Vault IDs allow you to label your secrets. This is useful if you're managing secrets across multiple environments (like dev and prod) or just want clearer vault handling. Let's try it from scratch. First, create a new password file to use with our Vault ID.
```bash
    echo 'qwerty' > ~/mycode/.vault_dev
```

Now create a brand new file to encrypt 
```bash
    vim ~/mycode/vars/vaultidtest.yml
```

```yaml
---
vaultid: success
```

Encrypt the file using the --vault-id option. This sets the ID and ties the password file to that ID.
```bash
    ansible-vault encrypt --vault-id dev@~/mycode/.vault_dev ~/mycode/vars/vaultidtest.yml
```

Now create a playbook that uses this encrypted file.
```yaml
---
- name: Vault ID test
  hosts: localhost
  connection: local
  gather_facts: no

  vars_files:
    - vars/vaultidtest.yml

  tasks:
    - name: show secret
      ansible.builtin.debug:
        msg: "{{ vaultid }}"
```

Run the playbook using the same Vault ID and password file:
```bash
    ansible-playbook --vault-id dev@~/mycode/.vault_dev ~/mycode/playbook-vaultid.yml
```








