# Ansible Callback Plugins
To control the output of the playbook from invocation until the **PLAY RECAP** statistics. Suppose you wanted to simplify the output for those individuals that might only be running playbooks. Or maybe you want the results of the playbook returned as JSON. Callback plugins are the solution.

Callback plugins may be activated one at a time from within ```ansible.cfg```. Below are several permutations to test. The list of possible plugins can be found within the Ansible Documentation on callbacks.

Read about "callback" plugins here:
https://docs.ansible.com/ansible/latest/plugins/callback.html

```shell
[defaults]
host_key_checking=no
nocows=True

# DENSE CALLBACK
# activate callback plugin (one at a time)
#stdout_callback = dense

# JSON CALLBACK
# activate callback plugin (one at a time)
#stdout_callback = json

# NULL CALLBACK
# activate callback plugin (one at a time)
#stdout_callback = null

# LOG_PLAY CALLBACK
# activate callback plugin (one at a time)
#stdout_callback = log_plays
[callback_log_plays]
# this is a FOLDER not a file. Ansible will create a log file PER host
log_folder = /tmp/hosts/  
```