# Ansible : Playbook CockroachDB

The aim is to describe how to create cluster coachroachdb instances. This project uses code shared by wikitops/ansible_cockroach team. Many thanks!

## Getting Started

To create cluster of VMs on Oracle VirtualBox, use Vagrant as instructed.
If there's already a cluster created such as Tanzu Kubernetes, use instructions to prepare hosted K8s.
Then run ansible playbook to create 

### Install Vagrant

*   Select [Vagrant](https://www.vagrantup.com/docs/installation/) for version of Linux as required
*   Update the Vagrant file based on your computer (CPU, memory), if needed. Note this version provision the public key to simply ssh
*   If running on windows, turn off hypervisor

### Create Clusters on OpenBox

```bash
$ vagrant box add https://app.vagrantup.com/ubuntu/boxes/bionic64
```

```bash
$ cd to ansible_cockroachdb
$ vagrant init
$ vagrant up
```
After build, check to see the VM clusters a\\
```bash
$ vagrant status
```

If everything run as expected, you should see something like this :

Current machine states:

cockroachd01                   running (virtualbox)
cockroachd02                   running (virtualbox)
cockroachd03                   running (virtualbox)



#### ssh into one of the VMs
```bash
$ vagrant ssh cockroachdb01
```
or using ssh on windows 10
```bash
$ ssh -i ./id_rsa vagrant@10.0.5.31
```

#### Install ansible if required (ubuntu/bionic)
```bash
$ sudo apt-get update
$ sudo apt install software-properities-commmon
$ sudo add-apt-repository ppa:ansible/ansible
$ sudo apt install ansible
```
#### if running ansible playbook from Linux, pull down ansible code
```bash
$ sudo git clone https://githubcom/$kc105/ansible_cockroachdb.git
```
```bash
$ ansible all -m ping -i ./hosts --private_key ./id_rsak
```
This playbook has some dependencies to other roles that must be downloaded before executing the playbook :

```bash
$ ansible-galaxy install -r requirements.yml
```

This command should download the NTP role from Wikitops Github account to the local role path.

To deploy the CockroachDB cluster on Vagrant, you just have to run the Ansible playbook cockroachdb.yml with this command :

```bash
$ ansible-playbook cockroachdb.yml --private_key ./id_rsak
```

If everything run ass expected, you should access the CockroachDB Web interface : http://10.0.5.31:7005/

#### if running ansible playbook using Azure DevOps
more to come...

#### Destroy

To destroy the Vagrant resources created, just run this command :

```bash
$ vagrant destroy
```


