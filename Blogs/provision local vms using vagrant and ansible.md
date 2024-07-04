Are you tired of having to go through the installation process every time you need a new Linux virtual machine? Do you hate the tedious cycle of creating snapshots for configuration changes, or worse, forgetting to snapshot and having to reinstall everything?

Enter Vagrant and Ansible, a powerful combination that lets you automate VM provisioning and configuration, saving you time and frustration. Vagrant works with different hypervisors (providers in Vagrant terminology), and we'll be focusing on VirtualBox, the default option.
# Installation
i'm going to cover installation for Debian/Ubuntu based systems, as this is what am using, 
we are going to install:
- vagrant
```bash
wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update && sudo apt install vagrant
```
- ansible:
```bash
sudo apt update
sudo apt install software-properties-common
sudo add-apt-repository --yes --update ppa:ansible/ansible
sudo apt install ansible
```
- virtualbox:
```bash
sudo apt update
# uncomment whichever you wanna install
#sudo apt install virtualbox # this might be an older version
#sudo apt install virtualbox-7.0 # this is the latest version in the time of writing
```
[alternative installation methods of virtualbox](https://itsfoss.com/install-virtualbox-ubuntu/)

you can find installation process for different operating systems in the links below:
- [Vagrant](https://developer.hashicorp.com/vagrant/install).
- [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/installation_distros.html).
- [VirtualBox](https://www.virtualbox.org/wiki/Downloads).

# Getting started
in my case i want to provision a kali linux vm for pentesting.
a quick to get started is to initialize the project using `vagrant init` command.
- First make a new directory and move into it:
```bash
mkcd vagrant_kali
```
> Tip Of The Day
	`mkcd`?? i know you probably never seen it before, because it is a custom bash function that basically just create a directory and cd into it.
	```bash
	mkcd () {
	        mkdir -p -- "$1" && cd -P -- "$1"
	}
	```
	add this function to your `~/.bashrc` or `~/.zshrc` and you will be able to create and cd into a directory with one command.

- Initialize the project :
```bash
vagrant init kalilinux/rolling
```
`kalilinux/rolling` is the name of kali linux vagrant box

> **What is a box?**
> a box is base image, basically like a clone of the virtual machine. that vagrant uses.
> you can search for the box of the operating system you want in [HashiCorp's Vagrant Cloud box catalog](https://vagrantcloud.com/boxes/search).

You now have a `Vagrantfile` pre-populated with comments and examples
> `Vangrantfile` contents

 ```ruby
# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
# The most common configuration options are documented and commented below.
# For a complete reference, please see the online documentation at
# https://docs.vagrantup.com.

# Every Vagrant development environment requires a box. You can search for
# boxes at https://vagrantcloud.com/search.
config.vm.box = "kalilinux/rolling"

# Disable automatic box update checking. If you disable this, then
# boxes will only be checked for updates when the user runs
# `vagrant box outdated`. This is not recommended.
# config.vm.box_check_update = false

# Create a forwarded port mapping which allows access to a specific port
# within the machine from a port on the host machine. In the example below,
# accessing "localhost:8080" will access port 80 on the guest machine.
# NOTE: This will enable public access to the opened port
# config.vm.network "forwarded_port", guest: 80, host: 8080

# Create a forwarded port mapping which allows access to a specific port
# within the machine from a port on the host machine and only allow access
# via 127.0.0.1 to disable public access
# config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

# Create a private network, which allows host-only access to the machine
# using a specific IP.
# config.vm.network "private_network", ip: "192.168.33.10"

# Create a public network, which generally matched to bridged network.
# Bridged networks make the machine appear as another physical device on
# your network.
# config.vm.network "public_network"

# Share an additional folder to the guest VM. The first argument is
# the path on the host to the actual folder. The second argument is
# the path on the guest to mount the folder. And the optional third
# argument is a set of non-required options.
# config.vm.synced_folder "../data", "/vagrant_data"

# Disable the default share of the current code directory. Doing this
# provides improved isolation between the vagrant box and your host
# by making sure your Vagrantfile isn't accessible to the vagrant box.
# If you use this you may want to enable additional shared subfolders as
# shown above.
# config.vm.synced_folder ".", "/vagrant", disabled: true

# Provider-specific configuration so you can fine-tune various
# backing providers for Vagrant. These expose provider-specific options.
# Example for VirtualBox:
#
# config.vm.provider "virtualbox" do |vb|
#   # Display the VirtualBox GUI when booting the machine
#   vb.gui = true
#
#   # Customize the amount of memory on the VM:
#   vb.memory = "1024"
# end
#
# View the documentation for the provider you are using for more
# information on available options.

# Enable provisioning with a shell script. Additional provisioners such as
# Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
# documentation for more information about their specific syntax and use.
# config.vm.provision "shell", inline: <<-SHELL
#   apt-get update
#   apt-get install -y apache2
# SHELL
end

```
this file gives you an overview of the main options available in `VagrantFile`
this is the VagrantFile i ended up with
```ruby
Vagrant.configure("2") do |config|
  config.vm.box = "kalilinux/rolling"
  config.vm.box_version = "2024.2.0"
  config.vm.network "private_network", ip: "192.168.56.10"
  config.vm.hostname = "machine"
  config.ssh.insert_key = false
  config.vm.disk :disk, size: "35GB", primary: true

  config.vm.provider "virtualbox" do |v|
	# set up vm name in virtualbox
    v.name = "kali-machine"
    # Display the VirtualBox GUI when booting the machine
    v.gui = true
    v.memory = 8192
    v.cpus = 6
  end

  # Set the name of the VM. See: http://stackoverflow.com/a/17864388/100134
  config.vm.define :kali_machine do |kali_machine|
  end

# Ansible config
  config.vm.provision "ansible" do |ansible|
	# Ansible playbook path
    ansible.playbook = "provisioning/playbook.yml"
	# Minimum version of ansible
    ansible.compatibility_mode = "2.0"
	# enables priviliege escation(sudo) for ansible
    ansible.become = true
  end
end

```
# Ansible playbook
- now we will create the playbook in the path mentioned in `Vagrantfile` `provisioning/playbook.yml`
```yaml
- hosts: all
  become: yes
  roles:
  - kali-init

```
roles are a file structure that lets load automatically tasks...
roles also help make the playbook more structured as it grows big
now we have one role and its structure look like this:
```
roles
└── kali-init
	└── tasks
		├── main.yml
		├── packages.yml
		└── tor.yml
```

`tasks/main.yml`
```
- import_tasks: packages.yml
  become: yes
- import_tasks: tor.yml
  become: yes
```

`tasks/packages.yml`
```yaml
- name: Download packages using apt
  apt:
    update_cache: yes
    name:
      - neovim
      - curl
      - wget
      - nmap
      - wireshark
      - tor
      - proxychains
      - torbrowser-launcher
    state: present
  become: yes

```

`tasks/tor.yml`
```yaml
- name: Ensure Proxychains is installed
  apt:
    name: proxychains
    state: present

- name: Ensure tor is installed
  apt:
    name: tor
    state: present

- name: Enable tor service
  ansible.builtin.systemd:
    name: tor
    state: started
    enabled: true

- name: Backup current proxychains.conf
  copy:
    src: /etc/proxychains.conf
    dest: /etc/proxychains.conf.bak
    remote_src: yes

- name: Uncomment dynamic_chain
  replace:
    path: /etc/proxychains.conf
    regexp: '^#dynamic_chain'
    replace: 'dynamic_chain'

- name: Uncomment proxy_dns
  replace:
    path: /etc/proxychains.conf
    regexp: '^#proxy_dns'
    replace: 'proxy_dns'

- name: Comment random_chain
  replace:
    path: /etc/proxychains.conf
    regexp: '^random_chain'
    replace: '#random_chain'


- name: Comment strict_chain
  replace:
    path: /etc/proxychains.conf
    regexp: '^strict_chain'
    replace: '#strict_chain'

- name: Modify proxychains configuration
  lineinfile:
    path: /etc/proxychains.conf
    line: 'socks5 127.0.0.1 9050'
    state: present

- name: Modify proxychains configuration
  lineinfile:
    path: /etc/proxychains.conf
    line: 'socks4  127.0.0.1 9050'
    state: present

```

the project directory structure should look like this:
```
.
├── provisioning
│   ├── playbook.yml
│   └── roles
│       └── kali-init
│           └── tasks
│               ├── main.yml
│               ├── packages.yml
│               └── tor.yml
└── Vagrantfile

```
# Using vagrant
to provision a new vm, make sure you are in the directory where the `Vagrantfile` is and run:
```bash
vagrant up
```
![[Pasted image 20240704020743.png]]
the machine will get installed and spawned up, the gui will show up. After booting up ansible will connect to the vm and run playbook.
![[Pasted image 20240704021450.png]]![[Pasted image 20240704021658.png]]
this the output of ansible playbook finishing succesfully
![[Pasted image 20240704021941.png]]
the kali vm is now installed and running
**N.B**
	default user is `vagrant` and default password is also `vagrant`

to pause the vm run:
```
vagrant halt
```
to destroy run:
```
vagrant destroy
```