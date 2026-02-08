# Building and Using Your Own Ansible Collection
Collections are used to package and share roles, modules, and other automation content. By creating a collection, you can neatly organize your custom tools, distribute them to others, and simplify content reuse.

Official documentation for collection structure is available [here](https://docs.ansible.com/ansible/devel/dev_guide/developing_collections_structure.html).

Use the `ansible-galaxy` command to initialize a collection. This sets up a collection structure for you
```bash
    ansible-galaxy collection init alta3.mycollection
```

```text
    The alta3 part is the namespace, which is just a way to organize your content. The mycollection part is the name of your collection.
```

Build your collection to create a distributable tarball. This step packages all your content into a compressed file for easy sharing or installation:
```bash
    ansible-galaxy collection build
```

```text
    This creates a .tar.gz file in your collection directory. The version of the collection is defined in galaxy.yml.
```

Install your collection to test it.

```bash
    ansible-galaxy collection install alta3-mycollection-1.0.0.tar.gz
```

Verify that your collection is installed:
```bash
    ansible-galaxy collection list | grep alta3
```
