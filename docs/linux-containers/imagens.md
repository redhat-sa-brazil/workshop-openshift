
# O que são imagens e como funcionam

As  imagens são a base para a execução de contêineres.
A imagem é um pacote de sistema de arquivos
que contém todas as dependências necessárias para executar
um processo: **arquivos no sistema de arquivos,** **pacotes**
**instalados,** **recursos disponíveis, processos em execução**
**e módulos do kernel.**
Os contêineres em execução usam uma visualização imutável da
imagem, permitindo que vários contêineres utilizem a mesma imagem
simultaneamente. Como as imagens são arquivos, elas podem ser gerenciadas
por sistemas de controle de versão, aprimorando a automação no contêiner
e o provisionamento de imagens.

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

<https://hub.docker.com>

<https://registry.access.redhat.com>

<https://registry.fedoraproject.org>
