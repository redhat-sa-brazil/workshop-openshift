# Uso das interfaces Web Console e 'oc'

Com a interface da linha de comandos (CLI) do OpenShift, você pode criar aplicativos e gerenciar projetos OpenShift a partir de um terminal. A CLI é ideal em situações em que você está:

- Trabalhando diretamente com o código fonte do projeto.

- Operações de script do OpenShift.

- Restrito aos recursos de largura de banda e não pode usar o console da web.

A CLI do OpenShift está disponível usando o comando oc:

```
$ oc < comando >
(...)
```

Caso você queira instalar na sua máquina local, você pode baixar e descompactar a CLI com uma assinatura ativa do OpenShift Enterprise no Red Hat Customer Portal ou através do link: <https://mirror.openshift.com/pub/openshift-v4/clients/ocp/latest/>

## Efetuando login na CLI

Você pode efetuar login na oc CLI para acessar e gerenciar seu cluster.

### Pré-requisitos

- Você deve ter acesso a um cluster da Plataforma OpenShift Container.
- Você deve ter instalado a CLI.

#### Procedimento

Efetue login na CLI usando o comando oc login e insira as informações necessárias quando solicitado.

```
$ oc login
Server https://seu-link
The server uses a certificate signed by an unknown authority.
You can bypass the certificate check, but any data you send to the server could be intercepted by others.
Use insecure connections? (y/n): y

Authentication required for https://seu-link (openshift)
Username: <<username>>
Password:
Login successful.

You don't have any projects. You can try to create a new project, by running

    oc new-project <projectname>

Welcome! See 'oc help' to get started.
```

Agora você pode criar um projeto ou emitir outros comandos para gerenciar seu cluster.

## Criando um projeto

Use o command new-project para criar um novo projeto.

```
$ oc new-project openshift-demo
Now using project "openshift-demo" on server "https://seu-link".
```

## Criando um novo aplicativo

```
$ oc new-app https://github.com/redhat-sa-brazil/demo-openshift-python.git' --name='web'
(...)
```

## Visualizando pods

Use o comando oc get pods para visualizar os pods do projeto atual.

```
$ oc get pods
NAME                  READY   STATUS      RESTARTS   AGE     IP            NODE                           NOMINATED NODE
<<nome do pod>>       0/1     Completed   0          5m45s   10.131.0.10   <<identificação do node>>      <none>
(...)
```

## Escalando pods

Use o comando oc pods para escalar um pod específico.

```
$ oc scale dc web --replicas=2
(...)
```

## Expondo o componente

Use o comando oc expose para criar uma rota pública e expor o componente web.

```
$ oc expose service/web --hostname='demo.apps.ocp.acme.com'
(...)
```

## Listando recursos de API suportados

Use o comando oc api-resources para visualizar a lista de recursos da API suportados no servidor.

```
$ oc api-resources
(...)
```

Pode pode ainda usar o comando oc explain para explicação de cada _api-resource_.

## Ajuda

Adicionalmente, você pode obter ajuda com os comandos da CLI e os recursos da OpenShift Container Platform das seguintes maneiras:
Use oc help para obter uma lista e descrição de todos os comandos da CLI disponíveis:

```
$ oc help

OpenShift Client

This client helps you develop, build, deploy, and run your applications on any
OpenShift or Kubernetes cluster. It also includes the administrative
commands for managing a cluster under the 'adm' subcommand.

Usage:
  oc [flags]

Basic Commands:
  login           Log in to a server
  new-project     Request a new project

(...)
```

Você ainda pode usar o sinalizador --help para obter ajuda sobre um comando específico da CLI:

```
$ oc create --help

Create a resource from a file or from stdin.

 JSON and YAML formats are accepted.

Usage:
  oc create -f FILENAME [flags]
(...)
```

## Desconectando-se da CLI

Você pode desconectar a CLI para encerrar sua sessão atual.
Use o comando oc logout.

```
$ oc logout
(...)
```

Isso exclui o token de autenticação salvo do servidor e o remove do seu arquivo de configuração.

Se você quiser saber mais sobre os comandos oc , como Developer CLI commands  e Administrator CLI commands basta acessar o link <https://docs.openshift.com/container-platform/4.2/cli_reference/openshift_cli/getting-started-cli.html> e será direcionado para documentação na qual explica cada um dos comandos disponíveis a serem usados no terminal.
