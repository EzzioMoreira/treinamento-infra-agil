# Desabilitar SELinux
vim /etc/selinux/config

SELINUX=disabled

# Desabilitar FW
systemctl stop firewalld

systemctl disable firewald

# Install puppet agent
sudo yum install puppet-agent

sudo /opt/puppetlabs/bin/puppet resource service puppet ensure=running enable=true
