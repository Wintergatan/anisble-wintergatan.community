# wintergatan.community

This is our Ansible repo for managing host that reside under wintergatan.commuinity. We currently have following branches:
- main  : Production management. This represents live Systems 
- devel : Development management. This is for testing new features, and providing development systems.

Ansible is used for configuration management and broken down into three major parts. Inventory, Playbooks, and Roles. we will cover these three briefly. Anyone looking for a more in-depth documentation on ansible should checkout [the docs](http://docs.ansible.com/modules.html).

## Inventory

An inventory is a document that describes all of the hosts you want to manage, and how they are grouped. Take a look at our [production inventory](/production.inventory) to get a sense of the structure.

This allows us to slice and dice boxes. For instance all our boxes might share a common configuration like backups and common userland tools, but only a subset will need to be setup as a web server. This allows us to address each group of machines separately.

## Roles

From the ansible glossary, "Roles are units of organization in Ansible". This can be everything from an nginx role to make sure that nginx is setup and configured, to a role that will make sure a service gets deployed on a box and restarted.

## Playbooks

Playbook bind it all together. In a playbooks you assign a number of roles to an inventory group, or host. Most of the time you are running playbooks to actually make things happen.


# How we use Ansible
We manage our systems with Ansible this assumes that whatever may get changed will survive another ansible run. If not it should've been in this repo. We _don't_ automatically run this repo against our machines simply to ensure that a rouge admin's git account can't directly push changes. Though we might make it semi automtic.

# Getting started

First install the collections and roles required for this repo.

```bash
ansible-galaxy install --roles-path ./roles/ -r requirements.yml
```

(Assuming you have root access to our Servers) You now can run playbooks against our servers. Or you can provide your own inventory for testing purpouses. You might want to try a ping first.

```bash
#ping all hosts
ansible -i [INVENTORY].inventory -m ping all
#Run [PLAYBOOK].play.yml with [INVENTORY].inventory
ansible-playbook -i [INVENTORY].inventory [PLAYBOOK].play.yml
``` 
