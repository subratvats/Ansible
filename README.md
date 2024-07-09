# Ansible

### Ansible use setup module to gather facts
#We can set ansible_connection inventory parameter value to localhost to tell Ansible to make a local connection instead of ssh. #Ans... winrm and ssh 


## varibale precedence

group var
host var
plabook level
extra var using cli (highest precedence)  # ansible-playbook playbook.yaml --extra-vars "dns_server=10.5.5.3"

![image](https://github.com/subratvats/Ansible/assets/65960496/f5ed6eda-7a6c-4f41-ac8f-b57807c429db)


## how to use output var on one task in to other task in ansible

The register keyword can capture various types of information, including stdout, stderr, rc (return code), and more. You can inspect the structure of the registered variable using the debug module to see all available fields.
```
---
- name: Example of using output variable from one task in another
  hosts: localhost
  gather_facts: no

  tasks:
    - name: Run a command and register its output
      command: echo "Hello, World!"
      register: echo_output

    - name: Display the output from the previous task
      debug:
        msg: "The output of the command was: {{ echo_output.stdout }}"

    - name: Use the output in a file
      copy:
        content: "Output of command: {{ echo_output.stdout }}"
        dest: /tmp/output.txt
```

and if we dont need to output and just want to see it we can run below with -v option 
```
ansible-playbook -i inventory playbook.yaml -v
```


## Magic variable

![image](https://github.com/subratvats/Ansible/assets/65960496/ed1e416f-0513-4c80-8eee-3aeae82d0554)
----------------------------------------
![image](https://github.com/subratvats/Ansible/assets/65960496/9b8499f1-a7b8-43b6-aa55-03f58a3f9a4a)
----------------------------------------
###### groups: list all the member in group
```
- name: List all hosts in a group
  debug:
    msg: "{{ groups['webservers'] }}"
```
###### group_names: Lists all groups the current host is part of.
```
- name: Display groups current host is part of
  debug:
    msg: "{{ group_names }}"
```
###### inventory_hostname: The name of the current host as defined in the inventory.
```
- name: Display current inventory hostname
  debug:
    msg: "{{ inventory_hostname }}"
```
###### inventory_hostname_short: The short name of the current host.
```
- name: Display current inventory hostname short
  debug:
    msg: "{{ inventory_hostname_short }}"
```
###### ansible_playbook_dir: The directory where the playbook is located.
```
- name: Display playbook directory
  debug:
    msg: "{{ ansible_playbook_dir }}"
```
###### ansible_role_names: List of roles applied to the current play.
```
- name: Display roles applied to the play
  debug:
    msg: "{{ ansible_role_names }}"
  ```
###### playbook_dir: Directory where the playbook file is located.
```
- name: Show playbook directory
  debug:
    msg: "{{ playbook_dir }}"
```
###### role_path: Directory of the current role.
```
- name: Show current role path
  debug:
    msg: "{{ role_path }}"
```
