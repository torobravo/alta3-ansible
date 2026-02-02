# alta3-ansible
Alta 3 Course: Introduction to Ansible

## Installing Ansible on Windows

Open a command prompt and load WSL (Windows Subsystem for Linux)
    1. Install Python (```sudo apt install python3```)
    2. Install Pip (```sudo apt install python3-pip```)
    3. Install Ansible (```pip install ansible```)

## Commands

To ping a remote host from the command line in Linux using Ansible

```Shell
    ansible fry -m ping
```
*fry* is the name of the remote host.

```Shell
    ansible fry -m ping -i ~/test_inventory1.ini
```
*-i* parameter is to specify the inventory file.  Otherwise set the path into .ansible.cfg file

To display the list of inventory or hosts run the following command:

```Shell
    ansible-inventory --list

    ansible-inventory --graph
```
