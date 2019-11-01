# Lab 1.0 - Preparar

## Lab 1.0 - Objetivos

Preparar o ambiente local para os próximos exercícios.

## Opções de execução

Você tem 2 opções disponíveis para a execução dos laboratórios. Consulte o instrutor para saber qual das opções abaixo você deve seguir.

### 1.0 Máquina Virtual local

Durante este workshop utilizaremos utilizaremos uma VM Linux como ambiente base dos laboratórios propostos aqui. Temos duas diferentes opções para obter e utilizar essa VM:

* **Virtual Box Appliance**: VM pré instalada e fornecida pelo Instrutor

  > [baixe aqui](https://drive.google.com/open?id=16CHefCCaXL9wfhsx6C7jgH11ODO5mFdP) \(`~845mb`\) ou peça ao instrutor o arquivo!

* **VM criada pelo aluno**: VM Criada pelo próprio aluno usando alguma ferramenta de Virtualização
  * Virtual Box

#### 1.0.1 - Instalar um virtualizador

Para conseguirmos montar um ambiente local sem interferir na sua máquina pessoal/profissional, recomendamos o uso de uma ferramenta de virtualização. Dentre as diversas opções, **recomendamos o VirtualBox**

* [**https://www.virtualbox.org**](https://www.virtualbox.org)

#### 1.0.2 - Criar a máquina virtual \(VM\)

Nos exercícios desse material vamos usar a Distro **CentOS 7**.

Após a instalação do virtualizador e a cópia do ISO do sistema operacional, vamos criar uma máquina virtual nas seguintes características:

* **CPU**: 2 vCPU
* **RAM**: 2G
* **HDD**: 2x 20GB
* **REDE**: Bridged Adapter \(escolher a NIC correta\)
* **SO**: Red Hat 64bits
* **BOOT**: ISO \(apontar pro caminho correto\)

#### 1.0.3 - Instalação do Sistema Operacional \(SO\)

Alguns passos importantes para a instalação:

* **Tenha certeza que somente um dos discos foi usado para instalar o sistema operacional!**

![](../.gitbook/assets/centos-install-disks.png)

* **Não instale nada além dos pacotes mínimos!**

![](../.gitbook/assets/centos-install-packages%20%281%29.png)

* **Não esqueça de dar um hostname e configurar a rede!**

![](../.gitbook/assets/centos-install-networking%20%281%29.png)

### 2.0 Máquina Virtual em um Cloud Provider

Siga as orientações passadas pelo Instrutor!

### 3.0 Instalação dos pacotes necessários para o Test Drive

Acesse a sua instância conforme explicado pelo seu instrutor e, logo após, com usuário `root` execute:

```text
yum install vim wget git bash-completion docker ansible -y
```

> INFO: Caso você não esteja como root, basta executar o comando abaixo. Qualquer problema chame o instrutor.
>
> ```text
> sudo -i
> ```

Em seguida habilite o serviço do Docker Daemon no SystemD

```text
systemctl enable docker
systemctl start docker
```

