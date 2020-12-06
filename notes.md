# Windows--vagrant requires hypervisor disabled. Also vagrant doesn't run with docker since docker uses hyper-v to create containers.

## using powershell on windows
$ get-windowsoptionalfeature -online
$ Disable-WindowsOptionalFeature -Online -FeatureName HypervisorPlatform
## if running into RPC_S_SERVER_UNAVAILABLE during virtual box start, it's beause hyper-v service blocks all other calls to VT hardware
### so try this using cmd (admin) on windows, reboot after each
bcdedit /set hypervisorlaunchtype off
bcdedit /set hypervisorlaunchtype on
bcdedit /set hypervisorlaunchtype auto


# vagrant
vagrant ssh cockroachdb01

# set up ansible on ubuntu
sudo apt-get update
sudo apt install software-properties-common
sudo add-apt-repository ppa:ansible/ansible
sudo apt install ansible

# clone git
sudo git clone https://github.com/kc105/ansible_cockroachdb.git

## ssh using private key without using vagrant
ssh -i ~/.ssh/id_rsa vagrant@ip_addr

## ping all
ansible all -m ping -i ./hosts --private_key ./id_rsa

## access cockroach via web interface
http://10.0.5.33:7005