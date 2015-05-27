# mesosphere-kit

The Mesosphere Kit aims to provide a simple way to quickly deploy a
Mesos cluster with several common frameworks in a VirtualBox
environment.  It helps to have a remedial understanding of the
Vagrantfile but more importantly, how to install and use Vagrant.

## Requirements

* 8GB of memory is more than enough, probably could get away with less.
* VirtualBox 4.3.x or later (http://www.virtualbox.org).
* Vagrant 1.7.x or later (http://www.vagrantup.com).
* Ansible 1.9.x or later. (http://docs.ansible.com/intro_installation.html#getting-ansible) 

## Instructions

1.  Install requirements (see above).
2.  `git clone https://github.com/tgreenyc/mesosphere-kit.git`
3.  `cd mesosphere-git`
4.  Choose between single or multi-node deployment.
5.  If multinode, then change to the `mesosphere-kit/multihost` directory. (see *Adding More
    Slaves* section below if you think your local machine has the
    horsepower!
6.  Run `vagrant up` and wait a little bit while Ansible auto-configures
    the environment.

## Adding More Slaves

1. From the root of the git repo, type `cd multihost`.
2. Open `Vagrantfile` and look for the *SLAVES* line:
snippet...
```
SLAVES = 1

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty64"
```
3. Modify SLAVES constant to increase the number of VM's
   provisioned/configured as slaves.  Be careful that you don't run out
of resources!

## Troubleshooting

Maybe you ran out of resources?  Open an issue if you'd like.
