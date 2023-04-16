 <img src="https://thedevopsrunner.netlify.app/images/logoDark.svg" alt="8ber" width="35%" /> 

# Ansible - Auto deploy Nexus

This is a simple ansible-playbook that automate the deployment of nexus artifactory on most of the **debian based linux distributions (i.e. that include apt)**. The playbook also validates that the nexus process has started on port 8081. 

The script is written using registered variables so it could withstand official sonatype future updates, and prevent errors based on the tar/binary file name. This is achieved by saving the output of a module and using it as a value by another variable. 

Specifically, the shell module is an example for an Ansible module that does not keep track of state. Thus, if a specific terms are due - error msg will appear. In order to be able to spin the playbook at all times, Ansible conditionals were used.

Note: this script is **NOT** meant to be used on AWS linux images.

## Usage

In order to use this script, please edit the <> file:

-
-
-

## Installation

1. Make sure your local machine has ansible installed. 
2. Make sure your linux target server has python (preferably version 3 installed)
```bash
python3 --version
```
3. in your local terminal:
```bash
ansible-playbook deploy-nexus.yaml
```
Note: You must verify ssh connection from your local machine to the target server.

## Featured modules:

- apt
- get_url (linux type)
- unarchive
- find
- shell
- when ("if statement")
- group
- user
- file
- lineinfile
- command
- wait_for
- debug

Further usages and parameters of the listed modules, can be found at the official [Ansible documentation](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/).
