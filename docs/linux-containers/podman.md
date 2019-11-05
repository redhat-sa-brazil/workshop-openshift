
# Uso do podman, buildah e skopeo no RHEL 8

Gerenciamento de contêineres com Podman
Contêineres, imagens e registros de imagens precisam interagir uns com
os outros. Por exemplo, você precisa ser capaz de criar imagens e colocá-las
em registros de imagens. Você também precisa ser capaz de recuperar uma
imagem do registro de imagens e criar um contêiner a partir dessa imagem.

![Podman](../images/123.png)

O _**Podman**_ é uma ferramenta open source para gerenciar contêineres e
imagens de contêiner e interagir com registros de imagens. Ele oferece
os seguintes recursos principais:
Ele usa o formato de imagem especificado pelo Open Container Initiative ( OCI )
. Essas especificações definem um formato de imagem padrão, orientado
pela comunidade e não proprietário.
O Podman armazena imagens locais em um sistema de arquivos local. Isso
evita arquitetura de servidor/cliente desnecessária ou ter daemons em execução
na máquina local.
O Podman segue os mesmos padrões de comando da CLI do Docker; portanto, não
é necessário aprender a usar um novo conjunto de ferramentas.
O Podman é compatível com o Kubernetes. O Kubernetes pode usar o Podman
para gerenciar seus contêineres.
Atualmente, o Podman está disponível apenas em sistemas Linux. Para instalar
o Podman no Red Hat Enterprise Linux 8, execute sudo yum install podman ou
sudo dnf install podman.

_**Buildah**_
é uma ferramenta que facilita a criação das imagens de containers.
Uma das principais funcionalidades do buildah é permitir que você crie
uma imagem de container de um container existente, de um Dockerfile ou
mesmo do zero. O resultado será uma imagem compatível com as diretrizes da OCI.
Assim, elas estarão prontas para rodar em qualquer mecanismo de container que
também esteja de acordo com o padrão da OCI(como Podman e Docker).
O pacote ‘buildah’ está disponível no módulo ‘container-tools’  no RHEL 8.
Para instalar o buildah no Red Hat Enterprise Linux 8, execute sudo yum -y
install buildah.
Após a instalação, você pode consultar o manual (man pages) para mais
detalhes de como utilizar os comandos e outras funcionalidades inclusas no pacote.

_**Skopeo**_
É uma ferramente similar ao Buildah de certa forma, já que você também pode
manipular e criar imagens com ela. A grande diferença é que com Skopeo, essas
operações são feitas sem o Docker daemon. Dessa forma, ainda é possivel criar
e copiar imagens, inspecionar containers, e executar outras funcionalidades
sem utilizar os comandos do pacote docker. Os registries ou remote repositories
podem incluir o Docker Registry, registros locais, Red Hat Quay ou OpenShift
Registries.
Para instalar o skopeo no Red Hat Enterprise Linux 8, execute sudo yum -y
install skopeo.
Após a instalação, você pode consultar o manual (man pages) para mais
detalhes de como utilizar os comandos e outras funcionalidades inclusas no pacote.







