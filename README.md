decision_node
=========

This role serves as a helper to take decisions in ansible based on variables coming from previous nodes

Install
-------

```
ansible-galaxy role install git+https://github.com/zaskan/decision_node.git
```

Use Example
--------------

Create a Job template which uses the following playbook:

```
- name: Test decisions role - Task 1
  hosts: localhost
  tasks:
    - name: Evaluate conditions
      ansible.builtin.set_stats:
        data:
          job_status: SUCCESS
          task_count: 4
```

Create a second Job template using the following. You can add the vars at play or Job Template level via extra vars.

```
- name: Test decisions role - Task 2
  hosts: localhost
  tasks:
    - name: Evaluate conditions
      ansible.builtin.include_role:
        name: decision_node
      vars:
        decision_node_conditions:
          - var_name: job_status
            operator: equals
            value: SUCCESS
          - var_name: task_count
            operator: greater_than
            value: 3
```
