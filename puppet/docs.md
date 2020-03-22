# Desabilitar SELinux
vim /etc/selinux/config

SELINUX=disabled

# Desabilitar FW
systemctl stop firewalld

systemctl disable firewalld

# Install puppet agent
- Ubuntu 18.04 Bionic Beaver
```
$ wget https://apt.puppetlabs.com/puppet5-release-bionic.deb
$ sudo dpkg -i puppet5-release-bionic.deb 
$ sudo apt update 
$ sudo apt install puppet-agent -y 
$ sudo /opt/puppetlabs/bin/puppet resource service puppet ensure=running enable=true
```
- Enterprise Linux 7
```
$ sudo rpm -Uvh https://yum.puppet.com/puppet5-release-el-7.noarch.rpm
$ sudo yum update -y
$ sudo yum install puppet-agent
$ sudo /opt/puppetlabs/bin/puppet resource service puppet ensure=running enable=true
```
# Export PATH

```
export PATH=/opt/puppetlabs/bin:$PATH
echo "export PATH=/opt/puppetlabs/bin:$PATH" >> /etc/bash.bashrc
```
