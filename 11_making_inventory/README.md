# Making an Inventory

Inventories are the foundation of using Ansible effectively, so this is an essential skill!

Right now, we have no way of connecting to any hosts. To prove this, let's use an Ansible ad-hoc command. An ad-hoc command is a way to run a quick task in Ansible without writing a playbook.

```bash
ansible fry -m ping
```
*Spoiler: This will fail because we haven’t told Ansible how to connect to these hosts yet!*

For Ansible to communicate with any hosts, it needs an "address book" of sorts... a host inventory! This inventory file contains all the information Ansible needs to SSH into a host and configure it. Inventories come in different formats, but let’s start with the INI format.

Create a file `test_inventory1.ini`:
```ini
[planetexpress]
bender      ansible_host=10.10.2.3 ansible_user=bender ansible_python_interpreter=/usr/bin/python3 fileuser=bender
fry         ansible_host=10.10.2.4 ansible_user=fry ansible_python_interpreter=/usr/bin/python3 fileuser=fry
zoidberg    ansible_host=10.10.2.5 ansible_user=zoidberg ansible_python_interpreter=/usr/bin/python3 fileuser=zoidberg
farnsworth  ansible_host=10.10.2.6 ansible_user=farnsworth ansible_ssh_pass=alta3 fileuser=farnsworth
```

| Part |	Description |
|--- |---
|planetexpress |	Group name for the hosts. You can use this group name to target multiple hosts.
|bender, fry, etc. |	Hostnames for the machines. These names can be ANYTHING!
|ansible_host |	The IP address or hostname Ansible uses to connect.
|ansible_user |	The username used to SSH into the machine.
|ansible_python_interpreter |	The path to the Python interpreter on the machine (Ansible executes Python code remotely).
|ansible_ssh_pass |	The password for SSH authentication (only used when password-based SSH is required).
|fileuser |	This is a totally random, CUSTOM variable unique to this user that you can reference in playbooks.

Let’s try the `ansible fry -m ping` command again, but this time point it to the inventory file using the `-i` flag.

```bash
ansible fry -m ping -i ~/test_inventory1.ini
```
*Success! You should see a response confirming that fry is reachable.*

Target the entire group by using the group name:
```bash
ansible planetexpress -m ping -i ~/test_inventory1.ini
```

If you ever run into issues with your inventory file, you can use the ansible-inventory command to check its contents.
```bash
ansible-inventory -i ~/test_inventory1.ini --list
```

Show the inventory structure as a graph:
```bash
ansible-inventory -i ~/test_inventory1.ini --graph
```

Get details about a specific host:
```bash
ansible-inventory -i ~/test_inventory1.ini --host fry
```

Adding `-i ~/test_inventory1.ini` to every command can get tedious. You can set a default inventory by editing your `.ansible.cfg` file in your home directory.
```ini
[defaults]
inventory = /home/student/test_inventory1.ini
```

Now, you can run commands without specifying the inventory file! 
```bash
ansible planetexpress -m ping
```

