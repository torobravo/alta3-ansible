# Advanced Variable Methods in Ansible (`vars_prompt`, `register`, `set_fact`)

Advanced ways to create and manage variables in Ansible.

| Tool |	Description	| Precedence |
|--- |--- |--- |
|`vars_prompt`	| Prompts the user to input variables during playbook execution. |	Medium-Low |
|`register`	| Captures task output and saves it as a variable for use in later tasks. |	Defined during execution |
|`set_fact`	| Dynamically creates or updates variables during playbook execution.	| Medium-High (overrides other s in the play) |

Ansible has some cool encryption options when prompting for variables, and for that we need `passlib`

```bash
python3 -m pip install passlib
```

### Explore vars_prompt
Let’s start with vars_prompt, which pauses the playbook to ask for input. This is handy for sensitive or dynamic values. We’ll prompt for a password, but note you could use this for any input you need!

Create `vim ~/mycode/prompt-playbook01.yml`

```yaml
---
- name: How to prompt for variables
  hosts: localhost
  gather_facts: no

  vars_prompt:
    - name: "yourpassword"
      prompt: "What is your password?"
      private: yes
      encrypt: "sha512_crypt"
      confirm: yes
      salt_size: 7
      default: "qwerty"

  tasks:
    - name: Print out the password
      debug:
        msg: "{{ yourpassword }}"
```

### Capturing Output with `register`
Let’s move on to `register`. This keyword saves the output of a task as a variable. You can use it later in the playbook to make decisions, display information, or run additional tasks.

```yaml
---
- name: Demonstrate register
  hosts: zoidberg
  tasks:
    - name: Install sl
      apt:
        name: sl
        state: present
        update_cache: yes
      register: apt_result
      become: true

    - name: Display full output
      debug:
        var: apt_result

    - name: Display specific parts of the output
      debug:
        msg: "The task changed: {{ apt_result.changed }}"
```

### Define Variables Dynamically with `set_fact`
The `set_fact` module lets you create or update variables during playbook execution. Let’s use it to get the current date and create a directory with that name.

```yaml
---
- name: Demonstrate set_fact
  hosts: localhost
  tasks:
    - name: Get the current date
      command: date +"%Y-%m-%d"
      register: result

    - name: Set a fact for the current date
      set_fact:
        date_now: "{{ result.stdout }}"

    - name: Create a directory with the current date
      file:
        path: "/tmp/newdir-{{ date_now }}"
        state: directory

    - name: Display the fact
      debug:
        msg: "Directory created with name: /tmp/newdir-{{ date_now }}"
```


