Ansible is a radically simple IT automation engine that automates cloud provisioning, configuration management, application deployment, intra-service orchestration, and many other IT needs.

Designed for multi-tier deployments since day one, Ansible models your IT infrastructure by describing how all of your systems inter-relate, rather than just managing one system at a time.

It uses no agents and no additional custom security infrastructure, so it's easy to deploy - and most importantly, it uses a very simple language (YAML, in the form of Ansible Playbooks) that allow you to describe your automation jobs in a way that approaches plain English.



Playbooks record and execute Ansible’s configuration, deployment, and orchestration functions. They can describe a policy you want your remote systems to enforce, or a set of steps in a general IT process.

If Ansible modules are the tools in your workshop, playbooks are your instruction manuals, and your inventory of hosts are your raw material.

At a basic level, playbooks can be used to manage configurations of and deployments to remote machines. At a more advanced level, they can sequence multi-tier rollouts involving rolling updates, and can delegate actions to other hosts, interacting with monitoring servers and load balancers along the way.

Playbooks are designed to be human-readable and are developed in a basic text language. There are multiple ways to organize playbooks and the files they include, and we’ll offer up some suggestions on that and making the most out of Ansible.

`brew install ansible`

 
     bash dir.sh
     echo $?
 
     curl -L https://www.chef.io/chef/install.sh | sudo bash
 
     

   37  pwd
   38  whoami
   39  sudo su -
 
   42  sudo rm -d /foo

   44  nano dir.rb
   45  sudo chef-client -z dir.rb

   49  python3 -m pip install --user ansible


   52  sudo apt update
   53  sudo apt install python3-pip
   54  python3 -m pip install --user ansible

   check for an ansible directory in /etc
   `ls -l | grep ansible`


mkdir: cannot create directory ‘ansible’: Permission denied
ubuntu@cfgmgmt:/etc$ sudo mkdir ansible
ubuntu@cfgmgmt:/etc$ ls -l | grep ansible
drwxr-xr-x 2 root root       4096 Aug 25 21:28 ansible
ubuntu@cfgmgmt:/etc$ 

`ansible --version`

ansible configuration file is only created automatically during the installation if you perform the 
installation with package managers like yum or apt-get. If you installed ansible using pip you should 
create the configuration file manually.


ubuntu@cfgmgmt:/$ cd /etc/ansible
ubuntu@cfgmgmt:/etc/ansible$ ls

ubuntu@cfgmgmt:/etc/ansible$ sudo touch ansible.cfg
ubuntu@cfgmgmt:/etc/ansible$ ls
ansible.cfg
ubuntu@cfgmgmt:/etc/ansible$ ansible --version
ansible [core 2.13.3]

  config file = /etc/ansible/ansible.cfg

  configured module search path = ['/home/ubuntu/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /home/ubuntu/.local/lib/python3.10/site-packages/ansible
  ansible collection location = /home/ubuntu/.ansible/collections:/usr/share/ansible/collections
  executable location = /home/ubuntu/.local/bin/ansible
  python version = 3.10.4 (main, Jun 29 2022, 12:14:53) [GCC 11.2.0]
  jinja version = 3.0.3
  libyaml = True

  local ip
   inet 192.168.0.37

`sudo vi /etc/hosts.txt`

`sudo vi /etc/ansible/ansible.cfg`

ubuntu@cfgmgmt:~$ `ansible all -m ping`
192.168.0.37 | UNREACHABLE! => {
    "changed": false,
    "msg": "Failed to connect to the host via ssh: ssh: connect to host 192.168.0.37 port 22: Connection timed out",
    "unreachable": true
}

ubuntu@cfgmgmt:~$ ansible all -m ping
192.168.0.37 | FAILED! => {
    "msg": "to use the 'ssh' connection type with passwords or pkcs11_provider, you must install the sshpass program"
}

`sudo apt install sshpass`

ubuntu@cfgmgmt:~$ ansible all -m ping
192.168.0.37 | UNREACHABLE! => {
    "changed": false,
    "msg": "Failed to connect to the host via ssh: ssh: connect to host 192.168.0.37 port 22: Connection timed out",
    "unreachable": true
}

`sudo apt update`
`sudo apt-get update`
`sudo apt-get upgrade`
