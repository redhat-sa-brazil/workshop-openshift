
# Automação de Build

No desenvolvimento de aplicações existe uma etapa denominada `build`, responsável por processar os artefatos produzidos pelos desenvolvedores e gerar o artefato final que será colocado em produção. Dado que estamos falando de aplicações em containers, ainda precisamos preparar uma imagem que contenha os pré-requisitos da aplicação e o artefato final gerado pela etapa de `build`.

Para aliviar a complexidade dessa atividade, o OpenShift contempla o componente [Source-to-Image](https://github.com/openshift/source-to-image), que é uma ferramenta para construir artefatos diretamente a partir da origem e injetar em imagens de contêiner base.

Para começar a experimentar essa automação, vamos criar um novo projeto para organizar nossos recursos. Substitua `instrutor` pelo seu usuário no laboratório (ex.: `aluno1`), e execute:

```bash
$ oc new-project instrutor-devx-workshop

Now using project "instrutor-devx-workshop" on server "https://api.ocp.dc1.rhbrlab.com:6443".
(...)
```

Agora já podemos criar nossa aplicação, que no caso foi escrita em Python. Ela se encontra em <https://github.com/redhat-sa-brazil/demo-openshift-python>, e **você precisa fazer um `fork` desse repositório para sua própria conta do Github**. Em seguida, execute:

```bash
$ oc new-app 'https://github.com/<usuário github>/demo-openshift-python.git' --name='web'

--> Found image 9600762 (3 weeks old) in image stream "openshift/python" under tag "3.6" for "python"
(...)
    Run 'oc status' to view your app.
```

Ao executar o comando anterior, o OpenShift vai inspecionar o repositório e ativar o processo que chamamos de `Build Automation`. Esse processo vai identificar o ambiente de execução da nossa aplicação (Python 3.6) e buscar uma imagem base suportada para ele. Em seguida ele vai usar do `Source-to-Image` para construir nosso artefato final e gerar a imagem de container. Para saber a situação atual (não se preocupe com os detalhes), execute o comando:

```bash
$ oc status

In project instrutor-devx-workshop on server https://api.ocp.dc1.rhbrlab.com:6443

svc/web - 172.30.178.233:8080
  dc/web deploys istag/web:latest <-
    bc/web source builds https://github.com/redhat-sa-brazil/demo-openshift-python.git on openshift/python:3.6
      build #1 running for about a minute - 8002325: Exemplo funcional para OpenShift 4 (Davi Garcia (davivcgarcia) <davivcgarcia@gmail.com>)
    deployment #1 waiting on image or update


2 infos identified, use 'oc status --suggest' to see details.
```

Por de trás do processo de `Build Automation`, a plataforma cria um recurso chamado `BuildConfig`. Este recurso é responsável por definir a imagem base de container e como o artefato final da aplicação `web` vai ser gerado, no caso a partir de uma fonte `Git`. Podemos pensar nele como um modelo a ser seguido toda vez que um processo de `Build` for necessário para aquela aplicação.

Podemos listar os `BuildConfig` disponíveis, executando:

```bash
$ oc get buildconfig

NAME   TYPE     FROM   LATEST
web    Source   Git    1
```

E podemos ver mais detalhes de um `BuildConfig` específico executando:

```bash
$ oc describe buildconfig/web

Name:        web
Namespace:    instrutor-devx-workshop
Created:    2 minutes ago
Labels:        app=web
Annotations:    openshift.io/generated-by=OpenShiftNewApp
Latest Version:    1

Strategy:    Source
URL:        https://github.com/redhat-sa-brazil/demo-openshift-python.git
From Image:    ImageStreamTag openshift/python:3.6
Output to:    ImageStreamTag web:latest

Build Run Policy:    Serial
Triggered by:        Config, ImageChange
Webhook GitHub:
    URL:    https://api.ocp.dc1.rhbrlab.com:6443/apis/build.openshift.io/v1/namespaces/instrutor-devx-workshop/buildconfigs/web/webhooks/<secret>/github
Webhook Generic:
    URL:        https://api.ocp.dc1.rhbrlab.com:6443/apis/build.openshift.io/v1/namespaces/instrutor-devx-workshop/buildconfigs/web/webhooks/<secret>/generic
    AllowEnv:    false
Builds History Limit:
    Successful:    5
    Failed:        5

Build    Status        Duration    Creation Time
web-1     complete     1m20s         2019-11-06 17:54:07 -0300 -03

Events:    <none>
```

Como parte da automação padrão do OpenShift, assim que criamos um `BuildConfig` o primeiro processo de `Build` é iniciado. Cada processo recebe um `ID`, que serve como versão do `Build`. Na saída anterior vemos que já temos o `Build` de `ID 1`.

Além disso, a plataforma já adiciona `Labels` para agrupar recursos quando criamos o `BuildConfig`, que são propagados para os `Builds`. Para listar os `BuildConfigs` e `Builds` da nossa aplicação, execute:

```bash
$ oc get buildconfigs,builds -l app=web

NAME                                 TYPE     FROM   LATEST
buildconfig.build.openshift.io/web   Source   Git    1

NAME                             TYPE     FROM          STATUS     STARTED         DURATION
build.build.openshift.io/web-1   Source   Git@8002325   Complete   4 minutes ago   1m20s
```

Por fim, podemos ver os logs dos processos de `Build` da nossa aplicação. Para tal, execute:

```bash
$ oc logs -f buildconfig/web

Cloning "https://github.com/redhat-sa-brazil/demo-openshift-python.git" ...
    Commit:    800232512f1b91ff1aedb32e822ce61a282593c7 (Exemplo funcional para OpenShift 4)
    Author:    Davi Garcia (davivcgarcia) <davivcgarcia@gmail.com>
    Date:      Thu Dec 21 02:40:57 2017 -0200
(...)
Push successful
```

Como todos os `Builds` são versionado, podemos recuperar essas informações também de processos de `Build` anteriores. Para tal, execute:

```bash
$ oc logs -f build/web-1

Cloning "https://github.com/redhat-sa-brazil/demo-openshift-python.git" ...
    Commit:    800232512f1b91ff1aedb32e822ce61a282593c7 (Exemplo funcional para OpenShift 4)
    Author:    Davi Garcia (davivcgarcia) <davivcgarcia@gmail.com>
    Date:      Thu Dec 21 02:40:57 2017 -0200
(...)
Push successful
```

Afinal o que significa a mensagem `Push successful`? Vamos ver em seguida...

**Próximo:** [Images e ImageStreams](/developer-experience/images-imagestreams)
