## Summary

This repository contains a set of different examples of ansible playbooks for automating Cisco ACI that were used during the **Automating Cisco ACI using Ansible** webinar delivered in EMEAR.

## Inventory

Two examples of invertories are provided, both in INI and YAML format. The inventory includes not only APIC but also leaf and spine switches, although those are not used in any of the playbooks provided in this repository.

## Demos

### Demo 01
The simplest example of an Ansible playbook for Cisco ACI, with no variables, no anchors and no flow controls at all.

### Demo 02
Building on top of previous demo, this playbook includes variables, which are defined both in inventory and in an external variable file referenced using **vars_files**. 

Also, delegate_to: localhost has been replaced by connection: local defined at the playbook level.

### Demo 03
Building on top of previous demo, this playbook uses YAML anchors to avoid repetition of the parameters that are common to all Cisco ACI modules.

This playbook also includes loops to execute plays/tasks multiple times iterating pver a list of bridge domains, as well as conditionals to execute certain plays/tasks only when bridge domain attributes match some specific conditions.

This playbook also demonstrate how Jinja templating language can be leveraged for some variable processing like in-line conditionals, string manipulations or setting default values.

### Demo 04
This demo replaces password-based authentication with certificate=based authentication using X509 certificates. It's included also a playbook that implements pushing the certificate to the APIC for an existing user called "orchestrator".

### Demo 05
Building on top of previous demos, this demo includes an extra playbook that implements an application profile with some EPGs and contracts. The configuration is not complete as it assumes that contract filters are already present in the APIC.

This demo demonstrate how multiple playbooks can be imported into another playbooks. It also demonstrate how we can use the **subelements** filter to loop over nested lists. 

### Demo 06
This demo demonstrate how **aci_rest**  module can be used for posting or querying Cisco ACI REST API when specific modules are not available for a certain class. It also demonstrate how the query option can be used and how the registered variables can be consumed in other tasks in the same playbook.

### Demo 07
This demo demonstrate how to create and use an **Ansible role** that deploys Cisco ACI configuration. This particular role is a very simple one that deploys a BD, subnet and EPG doing a 1:1 mapping, following a network-centric approach. The playbook contains two different ways of adding roles: the tradditional one (that does not work in this case, as explained in the webinar, and is commented out) and the dynamic reuse way using `include_roles`

## Instructions

These playbooks has been tested with Ansible 2.9 and Cisco ACI collection 2.0.0.

Cisco ACI ansible collection can be installed using the following command:

```
$ ansible-galaxy collection install cisco.aci
```

Cisco ACI ansible collection can be upgraded using either --force option or --upgrade option (available in 2.10+):

```
$ ansible-galaxy collection install cisco.aci --force
```

Before using these playbooks, ansible inventory needs to modified according to your environment. Demo01 has the password hard-coded in the playbook, it has been removed from the repository.

To run the playbooks:

```
$ ansible-playbook -i inventory-yaml demoXX/demoXX.yaml
```

