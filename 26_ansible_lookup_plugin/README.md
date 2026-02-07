# Ansible Lookup Plugin
The name sounds a bit more dramatic than it is, the TLDR on Lookup Plugins is they are used to return data from an outside source. Source types include csv files, flat files, URLs, MongoDB, RabbitMQ, and many more.

Looking up the contents of a file is as simple as, ```{{ lookup("file", "/tmp/file.txt") }}``` where the first value, file describes the type of data to be accessed, followed by the path.

Review more about Lookup Plugins here: https://docs.ansible.com/ansible/latest/plugins/lookup.html

To get a list of all the lookup plugins, run the following command. Translated, this command says, "list for me all of the plugins that are of the technology lookup"
```shell
    ansible-doc -t lookup -l
```

Get help on the ```url``` lookup plugin.
```shell
    ansible-doc -t lookup url
```