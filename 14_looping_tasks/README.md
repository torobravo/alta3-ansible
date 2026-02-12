# Understanding and Using the Loop Keyword in Ansible

Use the loop keyword in Ansible. You’ll see how it simplifies repetitive tasks, handles lists and complex data, and even overcomes limitations in certain modules.

### What is a loop, and why does it matter?
A loop in Ansible is a way to perform the same task multiple times, each time using a different value from a list or structure. Without loops, you’d have to manually write out repetitive tasks, which is inefficient and harder to maintain. Let's see this in action.

```yaml
- hosts: localhost
  tasks:
    - name: Print quotes
      debug:
        msg: "{{ item }}"
      loop:
        - "Roads? Where we're going, we don't need roads."
        - "If my calculations are correct, when this baby hits 88 miles per hour, you're gonna see some serious stuff."
        - "Your future is whatever you make it, so make it a good one."
```

### Understand the `item` keyword
When using a loop, the `item` keyword represents the current value being processed in the loop. It’s how you dynamically reference each value. Now that you understand the basics, let’s see how loops handle more complex data.

**`with_items`** vs. **`loop`** You may have seen in legacy code that instead of loop tasks use with_items. While with_items still works and isn't deprecated (yet) it does lack flexibility that the loop keyword introduced in Ansible 2.5- specifically, being able to loop over dictionaries!


