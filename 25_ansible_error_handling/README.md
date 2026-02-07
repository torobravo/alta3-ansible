# Ansible Error Handling
In 2.0, Ansible added a block feature to allow for logical grouping of tasks and even in-play error handling. Most of what you can apply to a single task can be applied at the block level, which also makes it much easier to set data or directives common to the tasks. The ```block``` may be further augmented by ```rescue``` and ```always```.

**block** - This is what you want to do. Blocks allow for logical grouping of tasks and in play error handling. Most of what you can apply to a single task (with the exception of loops) can be applied at the block level.

**rescue** - Why do we fall down? So we can learn to stand back up! Think of rescue as how you "stand back up" or "how to recover". If you do not encounter any failures within the rescue, your playbook will continue.

**always** - These tasks are always performed, even if your block and rescue sections encounter failures, you'll still perform these tasks.

By combining blocked tasks with rescue and always tasks, it is possible to create highly responsive playbook that's can rollback when they encounter an error. We'll explore some of those techniques in this lab.

### To inject a fail into a block

```shell
    #  Injecting a fail into the playbook           
    - name: Inject a fail
      ansible.builtin.shell: "/bin/false"
```
