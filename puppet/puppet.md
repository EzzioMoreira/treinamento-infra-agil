# Desabilitar SELinux
vim /etc/selinux/config

SELINUX=disabled

# Desabilitar FW
systemctl stop firewalld

systemctl disable firewalld

# Install puppet agent
- Ubuntu 18.04 Bionic Beaver
```
wget https://apt.puppetlabs.com/puppet5-release-bionic.deb
sudo dpkg -i puppet5-release-bionic.deb 
sudo apt update 
sudo apt install puppet-agent -y 
sudo /opt/puppetlabs/bin/puppet resource service puppet ensure=running enable=true
```
- Enterprise Linux 7
```
sudo rpm -Uvh https://yum.puppet.com/puppet5-release-el-7.noarch.rpm
sudo yum update -y
sudo yum install puppet-agent
sudo /opt/puppetlabs/bin/puppet resource service puppet ensure=running enable=true
```
- Export PATH

```
export PATH=/opt/puppetlabs/bin:$PATH
echo "export PATH=/opt/puppetlabs/bin:$PATH" >> /etc/bash.bashrc
```
# Install puppet server
``` 
puppet resource package puppetserver ensure=latest
```
- Os binários dos componentes do Puppet ficam centralizados no diretório /opt/puppetlabs. Já os arquivos de configuração ficam centralizados em /etc/puppetlabs:
- Alterar as configurações de memória a ser usada pela JVM durante a execução do Puppet server: No CentosOS/Red Hat edite o arquivo /etc/sysconfig/puppetserver e no Debian/Ubuntu edite o arquivo /etc/default/puppetserver.
```
Antes: JAVA_ARGS="-Xms2g-Xmx2g-XX:MaxPermSize=256m"

Depois: JAVA_ARGS="-Xms512m-Xmx512m-XX:MaxPermSize=256m"
```
- Com esta configuração são alocados até 512 MB para uso da JVM. Por padrão, são alocados 2 GB de memória. Após alteração reiniciar serviço.
```
systemctl restart puppetserver
```
# Camada de recursos do Puppet

- Para o Puppet, tudo o que existe no sistema operacional é um resource, que pode ser do tipo: arquivo, pacote, serviço, usuário, entre outros.
- O Puppet possui uma camada chamada de RAL (Resource Abstraction Layer). Nela, cada recurso pode ter um ou mais providers associados, que são responsáveis pelo gerenciamento do recurso. O RAL é quem fará o trabalgo de checar o sistema operacional e determinar o provider adequado para realizar instalação de um pacote, criaçao de usuário, trabalhar com serviços, etc. 
- Todo recurso tem certas características que o identificam. Exemplo.
 1. Um diretório tem um caminho e um dono.
 2. Um usuário possui um grupo.
 3. Um usuário possui um número identificador.
 - Essas caractéristicas são chamadas de atributos. O Puppet agrupa recursos e atributos semelhantes em resource types.
 - A combinação de resources, providers, resource type e atributos formam a RAL, onde os resources estão em alto nível e os providers ficam em baixo nível.
