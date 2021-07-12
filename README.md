# cardano-stake-pool
Configure a Cardano stake pool with Ansible.


# Prerequisites
* Ansible control node with Ansible >=2.9.2

# How to Run
Clone this repository on the Ansible control node. Make sure a public SSH key for the user running Ansible is installed on all managed node having passwordless sudo: 

```bash
$ sudo visudo
```

Append the following:

```
<USERNAME> ALL=(ALL) NOPASSWD: ALL
```

Use `ssh-copy-id` to install public key on managed nodes.

Next run the playbook:

```bash
$ ansible-playbook -v -i hosts.yml pool.yml
```
