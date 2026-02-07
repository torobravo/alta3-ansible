# Using Collections
Collections are bundles of Ansible content like modules, roles, and plugins, designed to simplify complex tasks and make automation easier. They’re like Ansible’s toolbox for specific devices, platforms, or APIs.

Collections can be downloaded from [Ansible Galaxy](https://galaxy.ansible.com/ui/), which is a central repository where you can find and share Ansible content.

If you find one that looks interesting, feel free to download it using the following command provided on the page
```shell
    ansible-galaxy collection install
```

Run this command to install it directly from GitHub:
```shell
    ansible-galaxy collection install git+https://github.com/csfeeser/nasa_api.git
```

Verify that the collection was installed by running:
```shell
    ansible-galaxy collection list | grep apod
```

Collections are typically installed in `/home/student/.ansible/collections/ansible_collections/`

