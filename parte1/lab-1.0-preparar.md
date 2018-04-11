# Lab 1.0 - Objetivos

* Preparar o ambiente local para os próximos exercícios.

# Opções de execução

Você tem 3 opções disponíveis para a execução dos laboratórios . Consulte o instrutor para saber qual das opções abaixo você deve seguir.

## 1.0 Para usuários de estação de trabalho com MS Windows

### 1.0.1 Cliente SSH

Instale um cliente SSH para acessar o _shell_ da VM que será utilizada durante todo o nosso workshop.

Existem duas opções de _SSH Client_ que recomendamos:

* [**PutTTY**](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)

  > baixe o arquivo `putty-64bit-0.70-installer.msi`

* [**Git Bash**](https://git-scm.com/download/win) \(incluso no GIT SCM for Windows\)

## 2.0 Máquina Virtual

Durante este workshop utilizaremos utilizaremos uma VM Linux como ambiente base dos laboratórios propostos aqui.

Temos três diferentes opções para obter e utilizar essa VM:

* **Cloud Provider**: ambiente pré configurado pelo Instrutor
* **Virtual Box Appliance**: VM pré instalada e fornecida pelo Instrutor

  > [baixe aqui](https://drive.google.com/open?id=16CHefCCaXL9wfhsx6C7jgH11ODO5mFdP) \(`~845mb`\) ou peça ao instrutor o arquivo!

* **VM criada pelo aluno**: VM Criada pelo próprio aluno usando alguma ferramenta de Virtualização

  * Virtual Box
  * KVM
  * VMware Fusion
  * etc

### 2.0.1 - Instalar um virtualizador

Para conseguirmos montar um ambiente local sem interferir na sua máquina pessoal/profissional, recomendamos o uso de uma ferramenta de virtualização. Dentre as diversas opções, **recomendamos o VirtualBox \(Windows/Mac\) ou o Virt-Manager/KVM \(Linux\):**

* [**https://www.virtualbox.org**](https://www.virtualbox.org)
* [**https://virt-manager.org**](https://virt-manager.org)

### 2.0.3 - Criar a máquina virtual \(VM\)

Nos exercícios desse material vamos usar o **CentOS**.

Após a instalação do virtualizador e a cópia do ISO do sistema operacional, vamos criar uma máquina virtual nas seguintes características:

* **CPU**: 2 vCPU
* **RAM**: 2G
* **HDD**: 2x 20GB
* **REDE**: Bridged Adapter \(escolher a NIC correta\)
* **SO**: Red Hat 64bits
* **BOOT**: ISO \(apontar pro caminho correto\)

### 2.0.4 - Instalação do Sistema Operacional \(SO\)

Alguns passos importantes para a instalação:

* **Tenha certeza que somente um dos discos foi usado para instalar o sistema operacional!**

![](/parte1/extras/centos-install-disks.png)

* **Não instale nada além dos pacotes mínimos!**

![](/parte1/extras/centos-install-packages.png)

* **Não esqueça de dar um hostname e configurar a rede!**

![](/parte1/extras/centos-install-networking.png)

### 2.0.5 - Instalar os pré-requisitos para trabalhar com containers

Recomendamos acessar o _shell_ da VM usando um _SSH client_ \(PuTTY ou Git Bash no caso do windows\).

Para isso abra seu SSH client, informe o IP da VM \(pode ser obtido através do comando `ip a s` executado dentro da janela da VM\) e faça a conexão informando usuário e senha.

> Caso necessite, peça ajuda ao instrutor!

#### 2.0.5.1 Update do S.O \(OPCIONAL!\)

Antes de começarmos a instalação do ambiente, precisamos garantir que todos os pacotes do sistema estejam atualizados:

```
# yum update -y
# systemctl reboot
```

#### 2.0.5.2 Instalação dos pacotes mínimos necessários

```
# yum install vim wget git bash-completion docker
```

#### 2.0.5.3 Preparação do Docker Storage no host \(OPCIONAL!\)

Antes de inicializarmos o runtime de containers, precisamos preparar o segundo disco para ser usado como registro local de imagens. Para tal, precisamos descobrir qual o dispositivo é o disco:

```
# lsblk
```

Depois precisamos editar o arquivo `/etc/sysconfig/docker-storage-setup`com o seguinte conteúdo \(adaptando o `vdb` ou `sdb` para o dispositivo em questão\):

```
STORAGE_DRIVER="devicemapper"
DEVS="sdb"
VG="docker"
```

Depois precisamos executar o utilitário para criar e configurar o storage do docker. Execute a linha de comando abaixo:

```
# docker-storage-setup
```

#### 2.0.5.4 Habilitando o Deamon do Docker Engine no host \(OPCIONAL!\)

Para finalizar, configuramos o Systemd para habilitar e inicializar o runtime:

```
# systemctl enable docker
# systemctl start docker
```

Caso queira confirmar que tudo está certo, execute:

```
# docker run hello-world
```

## 3.0 Para usuários com sua própria VM na nuvem

Acesse a sua instância conforme explicado pelo seu instrutor e, logo após, com usuário `root` execute:

```
yum install vim wget git bash-completion docker-1.12.6 ansible -y
```

> INFO: Caso você não esteja como root, basta executar o comando abaixo. Qualquer problema chame o instrutor.
>
> ```
> sudo su -
> ```

E adicione o docker no boot:

```
systemctl enable docker
systemctl start docker
```



