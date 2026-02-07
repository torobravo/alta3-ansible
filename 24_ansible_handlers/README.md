# Ansible Handlers and Listeners
This lab will demonstrate the Ansible handlers. As we’ve mentioned, modules should be idempotent and can relay when they have made a change on the remote system. Playbooks recognize this and have a basic event system that can be used to respond to change.

These ‘notify’ actions are triggered at the end of each block of tasks in a play, and will only be triggered once even if notified by multiple different tasks.

Those things listed under a ```notify``` section of a task are called handlers.

Handlers are lists of tasks, not really any different from regular tasks, that are referenced by a globally unique name, and are notified by notifiers. If nothing notifies a handler, it will not run. Regardless of how many tasks notify a handler, it will run only once, after all of the tasks complete in a particular play.

Check out some basic documentation on handlers: https://docs.ansible.com/ansible/latest/user_guide/playbooks_handlers.html

### Q: What is the purpose of a handler?
*A: Handlers are tasks that are only run if they are notified to run. Notifications are produced if a task within the task section reports a "change". Handlers only run once, even if they are notified to run multiple times. Typically, they are used to perform restarts on an application or system.*

### Q: What is a listener?
*A: A listener is a way to "group" together handlers.*