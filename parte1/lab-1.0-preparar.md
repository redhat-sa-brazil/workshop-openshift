# Lab 1.0 - Objetivos

* Preparar o ambiente local para os próximos exercícios.

# Tarefas

## Criando uma VM do zero
### 1.0.1 - Instalar um virtualizador

Para conseguirmos montar um ambiente local sem interferir na sua máquina pessoal/profissional, recomendamos o uso de uma ferramenta de virtualização. Dentre as diversas opções, **recomendamos o VirtualBox \(Windows/Mac\) ou o Virt-Manager/KVM \(Linux\):**

* [**https://www.virtualbox.org**](https://www.virtualbox.org)
* [**https://virt-manager.org**](https://virt-manager.org)

### 1.0.2 - Obter imagem de instalação

Nos exercícios desse material vamos usar o **Red Hat Enterprise Linux Server**, mas também podemos usar qualquer outra distribuição derivada, como CentOS ou Fedora.

Para obter uma subscrição gratuita para **uso em desenvolvimento**, basta se inscrever gratuitamente no programa ** Red Hat Developers**. Mais informações em:

* [**https://developers.redhat.com/products/rhel/download/**](https://developers.redhat.com/products/rhel/download/)

### 1.0.3 - Preparar a máquina virtual (VM)

Após a instalação do virtualizador e a cópia do ISO do sistema operacional, vamos criar uma máquina virtual nas seguintes características:

* **CPU**: 2 vCPU
* **RAM**: 2G
* **HDD**: 2x 20GB
* **REDE**: Bridged Adapter \(escolher a NIC correta\)
* **SO**: Red Hat 64bits
* **BOOT**: ISO \(apontar pro caminho correto\)

### 1.0.4 - Instalação do Sistema Operacional (SO)

Alguns passos importantes para a instalação:

* **Tenha certeza que somente um dos discos foi usado para instalar o sistema operacional!**

![](/parte1/extras/centos-install-disks.png)

* **Não instale nada além dos pacotes mínimos!**

![](/parte1/extras/centos-install-packages.png)

* **Não esqueça de dar um hostname e configurar a rede!**

![](/parte1/extras/centos-install-networking.png)

## Usando um VM pronta através do Vagrant
### 1.0.5 Obtendo uma assinatura __Red Hat Developer__

Acesse o endereço https://developers.redhat.com

![](/parte1/extras/rhdev-portal-registernewuser.png)

realize o Registro de uma nova Conta

![](/parte1/extras/rhdev-new-account.png)

Após criar sua conta, confirme através do link enviado para o seu email.

Verifique sua subscrição acessando: https://access.redhat.com/management
Realize o login com sua conta recém criada!
Clique em Subscriptions. Deve haver uma subscrição `Red Hat Enterprise Linux Developer Suite`

![](/parte1/extras/subscription-active.png)

Ainda nessa página

![](/parte1/extras/myactivesubs.png)

Copie o PooldID da sua subscrição!

![](/parte1/extras/subs-poolid.png)

### 1.0.6 Importando a VM através do Vagrant
Realize o download do Vagrant para a sua plataforma (Win, Linux ou Mac) acessando https://www.vagrantup.com/downloads.html

Após o Vagrant devidamente instalado:
 * instale o seguinte plugin

 ```
 vagrant plugin install vagrant-registration
 vagrant plugin list
 ```

 * copie diretório `vagrant-workshop` fornecido pelo instrutor para sua máquina local.

Na console, acesse o diretório `vagrant-workshop` Execute o seguinte comando em uma console:

```
vagrant box add rhel74-ocp-workshop ./rhel74-ocp-workshop.box
vagrant box list
```

Antes de subir a vm com Vagrant, abra o arquivo `Vagrantfile` e altere o seguinte trecho no final:

```
if Vagrant.has_plugin?('vagrant-registration')
  config.registration.username = 'seu login no developers.redhat.com'
  #config.registration.password = '<access.redhat.com password>'
  config.registration.pools = [ '8a85f98a5ffdXXXXXX15fff7a77e74ca1' ] # PoolID da sua subscrição!!!
end
```

Salve o arquivo.

### 1.0.6 Iniciando a VM usando o Vagrant
inicie a VM com o seguinte comando:

```
vagrant up
```

Após alguns minutos a VM deve subir (obseve a saída no terminal)

Acesse a console da VM via `ssh`

```
vagrant ssh
sudo -i
```

### 1.0.7 - Instalar os pré-requisitos para hospedar containers

Antes de começarmos a instalação do ambiente, precisamos garantir que todos os pacotes do sistema estejam atualizados:

```
# yum update -y
# systemctl reboot
```

> Caso tenha algum problema com o auto-registro através do Vagrant, realize o registro manualmente da seguinte forma.
>

 ```
 subscription-manager register --username=rhnuser --password=rhnpasswd
 subscription-manager list --available    Find valid RHEL pool ID
 subscription-manager attach --pool=pool_id
 ```

> 
> Adicione os seguintes repositórios para instalar o `docker`
>

 ```
 subscription-manager repos --enable=rhel-7-server-extras-rpms
 subscription-manager repos --enable=rhel-7-server-optional-rpms
 ```

Depois do servidor reiniciar, precisamos instalar os pacotes mínimos necessários:

```
# yum install vim wget git bash-completion docker
```

Antes de inicializarmos o runtime de containers, precisamos preparar o segundo disco para ser usado como registro local de imagens. Para tal, precisamos descobrir qual o dispositivo é o disco:

```
# lsblk
```

Depois precisamos editar o arquivo `/etc/sysconfig/docker-storage-setup`com o seguinte conteúdo (adaptando o `vdb` ou `sdb` para o dispositivo em questão):

```
STORAGE_DRIVER="devicemapper"
DEVS="vdb"
VG="docker"
```

Depois precisamos executar o utilitário para criar e configurar o storage do docker. Execute a linha de comando abaixo:

```
# docker-storage-setup
```

Para finalizar, configuramos o Systemd para habilitar e inicializar o runtime:

```
# systemctl enable docker
# systemctl start docker
```

Caso queira confirmar que tudo está certo, execute:

```
# docker run hello-world
```
