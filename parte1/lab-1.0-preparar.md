# Lab 1.0 - Objetivos

* Preparar o ambiente local para os próximos exercícios.

# Tarefas

### 1.0.1 - Instalar um virtualizador

Para conseguirmos montar um ambiente local sem interferir na sua máquina pessoal/profissional, recomendamos o uso de uma ferramenta de virtualização. Dentre as diversas opções, **recomendamos o VirtualBox \(Windows/Mac\) ou o Virt-Manager/KVM \(Linux\):**

* [**https://www.virtualbox.org**](https://www.virtualbox.org)
* [**https://virt-manager.org**](https://virt-manager.org)

### 1.0.2 - Obter imagem de instalação

Nos exercícios desse material vamos usar o **Red Hat Enterprise Linux Server**, mas também podemos usar qualquer outra distribuição derivada, como CentOS ou Fedora.

Para obter uma subscrição gratuita para **uso em desenvolvimento**, basta se inscrever gratuitamente no programa ** Red Hat Developers**. Mais informações em:

* [**https://developers.redhat.com/products/rhel/download/**](https://developers.redhat.com/products/rhel/download/)

### 1.0.3 - Preparar e instalar a máquina virtual

Após a instalação do virtualizador e a cópia do ISO do CentOS 7, vamos criar uma máquina virtual nas seguintes características:

* **CPU**: 2 vCPU
* **RAM**: 2G
* **HDD**: 2x 20GB
* **REDE**: NAT \(Padrão\)
* **SO**: Linux 64bits \(CentOS/RHEL\)
* **BOOT**: ISO do CentOS 7

Alguns passos importantes para a instalação:

* **Tenha certeza que somente um dos discos foi usado para instalar o sistema operacional!**

![](/parte1/extras/centos-install-disks.png)

* **Não instale nada além dos pacotes mínimos!**

![](/parte1/extras/centos-install-packages.png)

* **Não esqueça de dar um hostname e configurar a rede!**

![](/parte1/extras/centos-install-networking.png)

### 1.0.4 - Instalar os pré-requisitos para hospedar containers

Antes de começarmos a instalação do ambiente, precisamos garantir que todos os pacotes do sistema estejam atualizados:

```
# yum update -y
# systemctl reboot
```

Depois do servidor reiniciar, precisamos instalar os pacotes mínimos necessários:

```
# yum install vim wget git bash-completion docker
```

Antes de inicializarmos o runtime de containers, precisamos preparar o segundo disco para ser usado como registro local de imagens. Para tal, precisamos descobrir qual o dispositivo é o disco:

```
# lsblk
```

Depois precisamos editar o arquivo `/etc/sysconfig/docker-storage-setup`com o seguinte conteúdo:

```
STORAGE_DRIVER="devicemapper"
DEVS="vdb"
VG="docker"
```

* Observar a saída do comando lsblk qual o block device utilizar para o segundo disco. Por exemplo, vdb, sdb... 

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



