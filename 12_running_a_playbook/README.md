# Running a Playbook
Documentation regarding building Ansible Playbooks can be found here:
https://docs.ansible.com/ansible/latest/user_guide/playbooks.html

Another useful resource is the list of Ansible Keywords. Keywords are used to build playbook logic:
https://docs.ansible.com/ansible/latest/reference_appendices/playbooks_keywords.html

Running a playbook uses the `ansible-playbook` command, whereas running ad-hoc commands use the `ansible` command.
```bash
ansible-playbook ~/mycode/playbook-apt.yml
```


Read the documentation on the 'apt' module.
```bash
ansible-doc apt
```

