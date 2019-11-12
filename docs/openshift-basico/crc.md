# CodeReady Containers

CodeReady Containers é um projeto focado em provisionar um cluster OpenShift 4.0 ou mais recente no seu computador local. Esse cluster providencia um ambiente minimamente pronto para rodar o OpenShift seja para testes ou desenvolvimento.
CodeReady Containers possui o `crc` CLI para interagir com a máquina virtual do CodeReady que hospeda o OpenShift cluster.

## Requisitos

### Hardware

- 4 CPUs

- 8 GB de memória

- 35 GB de disco

_Nota: esses requisitos são necessários para rodar o CodeReady Containers. Dependendo da demanda do projeto, mais recursos serão necessários._

### SO

- Windows 10 ou mais novo

- MacOS 10.12 ou mais novo

- RHEL/CentOS 7.5 ou mais novo

### Pacotes

- Libvirt

- NetworkManager

## Usando CRC

Após baixar a última versão do CodeReady Containers, extrair o conteúdo para um diretório do seu `$PATH`, você ja pode instalar e começar a usar a `crc` cli.

Use o comando `crc setup` para performar as operações necessárias para provisionar o ambiente necessário e as máquinas virtuais no seu comutador local. Esse comando também criará o diretório `~/.crc/` caso não exista.

```
$ crc setup
(...)
```

Após o término do ultimo comando, você pode executar `crc start` para que o serviço do CodeReady Containers seja inicializado.

```
$ crc start
(...)
```

Após o serviço ser inicializado, o cluster local deveria estar pronto para receber as operações e comandos desejados. Por exemplo, a partir desse ponto, você pode inicializar o web console, configurar o serviço para ser explorado via `oc` cli, bem como acessar as funcionalidades providenciadas pelo CodeReady Containers através da sua CLI.

Mais informações sobre uso e comandos do CodeReady Containers: <https://code-ready.github.io/crc/#common-tasks_gsg>
