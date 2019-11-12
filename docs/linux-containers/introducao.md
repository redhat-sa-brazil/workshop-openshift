
# Introdução

## Afinal, o que são containers

A tecnologia de container Linux é, na verdade, um conjunto de capacidades
que permitem o isolamento e contenção de aplicações. Apesar da recente
exposição do termo, essa é uma tecnologia que vem sendo aprimorada desde
o UNIX, com o chroot, ou do BSD, com o Jails.

![Virtualizacao](../images/virtu.png)  ![Containers](../images/containers.png)

Ao contrário da tecnologia de virtualização que encapsula um
sistema operacional completo em cima de um hardware virtual
para usar como casulo para aplicações, containers usam de
funcionalidades nativas do kernel Linux
para garantir isolamento e contenção das aplicações,
como por exemplo:

- Namespaces:

Permite criar uma abstração de um recurso de sistema
global particular e fazê-lo aparecer como uma instância separada
para processos dentro de um namespace. Conseqüentemente,
vários containers podem usar o mesmo recurso simultaneamente
sem criar um conflito.

- Control Groups (cgroups):

Permite agrupar processos para fins
de gerenciamento de recursos do sistema. Os Cgroups alocam o
tempo da CPU, a memória do sistema, a largura de banda da rede
ou combinações destes entre os grupos de tarefas definidos
pelo usuário.

- SELinux:

Fornece uma separação segura, pois impede que os
processos raiz dentro do container interfiram com outros processos globais.

- Linux Capabilities:

Permite a limitação dos privilégios
disponíveis a processos que rodam como root em pequenos grupos de privilégios.
Desse modo, um processo rodando com privilégios de root pode ser limitado
a obter apenas as permissões mínimas que ele precisa para executar suas tarefas.

***

Apesar das diversas funcionalidades, existem situações que podem
não funcionar conforme esperado quando executamos, por exemplo,
um container com Ubuntu em um servidor hospedeiro rodando CentOS.
Vale sempre lembrar que, container é linux e sua execução depende
das bibliotecas e principalmente do kernel do host.
Há muitos mecanismos de contêiner disponíveis para gerenciar e executar
contêineres individuais, incluindo *Rocket, Drawbridge, LXC, Docker e Podman.*

__Veja abaixo algumas vantagens importantes para o uso de contêineres:__

- Baixa área de ocupação do hardware:

Os contêineres usam recursos internos do SO para criar um ambiente isolado
em que os recursos são gerenciados usando recursos do SO. Essa abordagem
minimiza a quantidade de sobrecarga de CPU e na memória em comparação a
um hipervisor de máquina virtual.

- Isolamento de ambiente:

Os contêineres funcionam em um ambiente fechado onde as alterações feitas
no SO de host ou outros aplicativos não afetam o contêiner. Como as bibliotecas
necessárias para um contêiner são autocontidas, o aplicativo pode ser executado
sem interrupções.

- Implantação rápida:

Os contêineres são implantados rapidamente porque não há necessidade
de instalar todo o sistema operacional subjacente.

- Implantação em múltiplos ambientes:

Em um cenário tradicional de implantação usando um único host,
qualquer diferença de ambiente pode interromper o aplicativo.
Ao usar contêineres, no entanto, todas as dependências de aplicativo
e configurações de ambiente são encapsuladas na imagem do contêiner.

- Reusabilidade:

Ao usar contêineres, não há mais a necessidade de manter
servidores de bancos de dados de produção e desenvolvimento separados.
Uma única imagem de contêiner é usada para criar instâncias do serviço
de banco de dados.

***

Apesar de ser uma tecnologia antiga, os containers ganharam mais popularidade
hoje em dia principalmente pela sua portabilidade. Soluções como Docker
ficaram realmente atrativas quando permitiram que um container pudesse
ser compartilhado entre infraestruturas heterogêneas. Isso foi possível
graças a criação do
conceito de imagem, que será nosso próximo tópico nesse guia.

## O que são imagens e como funcionam

A imagem é um pacote de sistema de arquivos que contém todas as dependências necessárias para executar um processo: **arquivos de  configuração, pacotes de sistema, bibliotecas, etc.**

![Imagem de Container](../images/imagem_container.png)

## Onde as imagens ficam armazenadas

As imagens do contêiner precisam estar disponíveis localmente
para que o tempo de execução do contêiner as execute, elas
geralmente são armazenadas e mantidas em um repositório de imagens.
Existem dois tipos de repositórios, ou registros, importantes
para armazenamento das imagens de containers: registro local (ou storage local)
e registros remotos (públicos/privados).

O **storage local** é um espaço de armazenamento especial que reside
no mesmo host que executa os containers. Esse é usado para armazenar
as imagens que serão usadas para executar containers nessa máquina,
servindo como uma camada de cache. Esse é o primeiro repositório a
ser consultado em busca de imagens.

Os **registros remotos** são servidores, públicos ou privados,
responsáveis por compartilhar imagens construidas por
entidades e/ou usuários. Estes registros podem permitir não
só o acesso para download de imagens, mas também envio
de imagens novas por usuários autenticados/autorizados.
Dentre os mais famosos temos:

<https://quay.io>

<https://hub.docker.com>

<https://registry.access.redhat.com>

<https://registry.fedoraproject.org>

## Laboratório

Toda instalação do Podman acompanha configurações dos registros remotos mais comuns, podemos ver isso por meio do comando abaixo, que nos dá a informação dos registros pré configurados.

```
$ podman info

[...]
registries:
  blocked: null
  insecure: null
  search:
  - registry.redhat.io
  - registry.access.redhat.com
  - quay.io
  - docker.io
[...]

```

Para buscar imagens nos registros configurados, usa-se:

```
$ podman search centos

INDEX       NAME                                                        DESCRIPTION                                       STARS   OFFICIAL   AUTOMATED
quay.io     quay.io/jdeathe/centos-ssh-haproxy                 ## Overview  This build uses the base image ...   0
quay.io     quay.io/reynn/ansible-centos                                                                         0
quay.io     quay.io/sdase/centos                                                                                 0
docker.io   docker.io/library/centos                           The official build of CentOS.                     5657    [OK]
docker.io   docker.io/pivotaldata/centos-gpdb-dev              CentOS image for GPDB development. Tag names...   10
                1                  [OK]
[...]
```

Nesse caso ele iá buscar as imagens do CentOS no registry.redhat.io, registry.access.redhat.com, quay.io e docker.io. Estes já vem pŕe configurados com o Podman.

Você também pode filtrar pelo número de estrelas que um repositório possui, para isso basta passar o parametro *--filter=stars=10*.
Abaixo a busca traz somente resultados que tenham mais que 10 estrelas.

```
$ podman search centos --filter=stars=10

INDEX       NAME                                        DESCRIPTION                                       STARS   OFFICIAL   AUTOMATED
docker.io   docker.io/library/centos                    The official build of CentOS.                     5657    [OK]
docker.io   docker.io/pivotaldata/centos-gpdb-dev       CentOS image for GPDB development. Tag names...   10
docker.io   docker.io/jdeathe/centos-ssh                OpenSSH / Supervisor / EPEL/IUS/SCL Repos - ...   114                [OK]
docker.io   docker.io/ansible/centos7-ansible           Ansible on Centos7                                125                [OK]
docker.io   docker.io/consol/centos-xfce-vnc            Centos container with "headless" VNC session...   100                [OK]
docker.io   docker.io/kinogmt/centos-ssh                CentOS with SSH                                   29                 [OK]
docker.io   docker.io/imagine10255/centos6-lnmp-php56   centos6-lnmp-php56                                57                 [OK]
docker.io   docker.io/tutum/centos                      Simple CentOS docker image with SSH access        44
docker.io   docker.io/centos/mysql-57-centos7           MySQL 5.7 SQL database server                     64
docker.io   docker.io/centos/postgresql-96-centos7      PostgreSQL is an advanced Object-Relational ...   39
docker.io   docker.io/centos/httpd-24-centos7           Platform for running Apache httpd 2.4 or bui...   26
```

## Baixando imagens dos registros

Além de nome, imagens possuem tags (sufixo separado por ':') que podem identificar versões ou variações de uma imagem específica. Para baixar uma imagem para o storage local de imagens, usa-se:

```
$ podman pull centos:7
[...]
```

É possível também baixar imagens de registries específicos quando especificamos isso na linha de comando. No exemplo abaixo utilizaremos o registry oficial da Red Hat.

```
$ podman pull registry.access.redhat.com/rhel-atomic

podman pull registry.access.redhat.com/rhel-atomic
Trying to pull registry.access.redhat.com/rhel-atomic...Getting image source signatures
Copying blob 72325e24e69c done
Copying blob be2a678047d5 done
Copying config d8bc85b978 done
Writing manifest to image destination
Storing signatures
d8bc85b978032f3af9b012900e9d4f1331c71500008b0d9a617fdbd8fcac902c
```

Para verificar quais imagens estão disponíveis localmente, usa-se:

```
$ podman images

REPOSITORY                               TAG      IMAGE ID       CREATED       SIZE
registry.access.redhat.com/rhel-atomic   latest   d8bc85b97803   4 weeks ago   80.9 MB
```

## Removendo imagens locais

Para remover as imagens do repositório local, usa-se:

```
$ podman rmi <ID/tag>
[...]
```

Vamos remover a imagem do rhel atomic baixado anteriormente:

```
$ podman imagens | grep rhel-atomic
[...]
```

Tendo o ID da imagem, podemos apagá-la:

```
$ podman rmi d8bc85b97803

$ podman images
REPOSITORY   TAG   IMAGE ID   CREATED   SIZE
```

Caso a imagem já esteja sendo utilizada por um container, o podman não irá executar a exclusão da imagem e retornará o ID do container para que você exclua o container e em seguida a imagem.

**Próximo:** [Podman, Buildah e Skopeo](/linux-containers/podman)
