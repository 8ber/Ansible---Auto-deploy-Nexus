# Ansible - Auto deploy Nexus

This is a simple ansible-playbook that automate the deployment of nexus artifactory on most of the **debian based linux distributions (i.e. that include apt)**. The playbook also validates that the nexus process has started on port 8081. 

The script is written using registered variables so it could withstand official sonatype future updates, and prevent errors based on the tar/binary file name. This is achieved by saving the output of a module and using it as a value by another variable. 

Specifically, the shell module is an example for an Ansible module that does not keep track of state. Thus, if a specific terms are due - error msg will appear. In order to be able to spin the playbook at all times, Ansible conditionals were used.

Note: this script is **NOT** meant to be used on AWS linux images.

## Usage and installation 

**make sure:**
1. your local machine has ansible installed. 
2. your linux target server has python installed (preferably version 3).
3. verify/configure ssh connection from your local machine to the target server.

to install:

4. Edit the hosts file:
`*** ansible_ssh_private_key_file=~/.ssh/id_rsa ansible_user=root` replace "***" with your target server ip.
5. in your local terminal:
```bash
ansible-playbook deploy-nexus.yaml
```

### Featured modules:

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

### Equivalent shell commands

To clarify the manual process that this playbook is executing:
```bash
apt update
apt install openjdk-8-jre-headless #specific version needed by Nexus
apt install net-tools

cd /opt
wget https://download.sonatype.com/nexus/3/latest-unix.tar.gz
tar -zxvf latest-unix.tar.gz

adduser nexus
chown -R nexus:nexus nexus 
chown -R nexus:nexus sonatype-work

vim nexus/bin/nexus.rc
run_as_user="nexus"

su - nexus
/opt/nexus/bin/nexus start

ps aux | grep nexus
netstat -lnpt
```
