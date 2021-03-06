# mesosphere-kit

The Mesosphere Kit aims to provide a simple way to quickly deploy a
Mesos cluster with several common frameworks in a VirtualBox
environment.  It helps to have a remedial understanding of the
Vagrantfile but more importantly, how to install and use Vagrant.

## Requirements

The operating system chosen for this project is Ubuntu 14.04 x86_64
(Trusty), which will be downloaded automatically by Vagrant.

* 8GB of memory is more than enough, probably could get away with less
* VirtualBox 4.3.x or later (http://www.virtualbox.org)
* Vagrant 1.7.x or later (http://www.vagrantup.com)
* Ansible 1.9.x or later (http://docs.ansible.com/intro_installation.html#getting-ansible) 

## Frameworks Included

* Marathon
* Chronos

(I can easily add more, just haven't had a need for others yet).

## Service Discovery

* Mesos-DNS is installed and running on the master node by default.
* Haproxy is installed, configured, and running on the master node by
  default.  NOTE: It is only configured to support inbound load
  balancing to deployed Marathon apps.  See 'haproxy-marathon-bridge'
  link below for details. 

## Deploying Docker Containers
* Slaves automatically will deploy and configure the Docker engine for
  consumption by Marathon.  The mesos-master host also includes an
  example JSON definition of an app template that can be used to deploy
  a lightweight container from Docker Hub.  Path to the file is
  `/root/docker_marathon.json`

## Instructions

1.  Install requirements (see above).
2.  `git clone https://github.com/tgreenyc/mesosphere-kit.git`
3.  `cd mesosphere-git`
4.  Choose between single or multi-node deployment.
5.  If multinode, then change to the `mesosphere-kit/multihost` directory. (see *Adding More
    Slaves* section below if you think your local machine has the
    horsepower!
6.  Run `vagrant up` for either single or multi-node configuration, and wait a little bit 
    while Ansible auto-configures the environment.

## Adding More Slaves

1. From the root of the git repo, type `cd multihost`.
2. Open `Vagrantfile` and look for the *SLAVES* line:
```ruby
SLAVES = 1

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty64"
```
3. Modify SLAVES constant to increase the number of VM's
   provisioned/configured as slaves.  Be careful that you don't run out
of resources!

## UI Access to Mesos and Frameworks

* Mesos - http://44.44.44.10:5050
* Marathon - http://44.44.44.10:8080 
* Chronos - http://44.44.44.10:4400

## Frequently Asked Questions

```
Q: Why isn't your automation idempotent?
A: I don't know what that means.

Q: What is haproxy-marathon-bridge and what does it do?
A: See https://docs.mesosphere.com/getting-started/service-discovery/
   for details.

Q: Why does it deploy so slowly?
A: If you don't have enough local resources then this is to be expected.
   However, it is strongly encouraged that you use vagrant-cachier to
   create a reusable local apt repository. 
```


## Troubleshooting

Maybe you ran out of resources?  Open an issue if you'd like.
