# Lab 2.x - Objetivos

* Colocar em produção um container construído anteriormente.
* Aprender sobre operação básica do ambiente.
* Criar aplicações de forma transparente
* Expor serviços internos e externos

# Tarefas

### 2.X.1 - Acesse o ambiente OpenShift

![](https://storage.googleapis.com/workshop-openshift/oc-login.gif)

### 2.X.2 - Deploy imagem do Docker Hub

![](https://storage.googleapis.com/workshop-openshift/deploy-docker-image.gif)

### 2.X.3 - Escolha a imagem

[https://hub.docker.com/r/davivcgarcia/workshop-openshift/](https://hub.docker.com/r/davivcgarcia/workshop-openshift/)

WARNING: Por questões de segurança a imagem não pode ser executada utilizando o usuário root.

### 2.X.4 - Crie a rota

Na interface web selecione a opção _create route._

### 2.X.5 - Tour pelo GUI do POD

![](https://storage.googleapis.com/workshop-openshift/pod-navigation.gif)

Selecione o pod e navegue entre as abas: `Details, Environment, Metrics, Logs, Terminal e Events`

### 2.X.6 - Scale up

Selecione o a seta para cima na lateral do pod, escalando para 2 pods no total.

Enquanto o círculo estiver na cor cinza indica que está sendo provisionado, quando  
o círculo estiver colorido de azul significa que o novo foi corretamente provisionado  
e já está pronto para receber novas requisições.

TIP: Os novos pods são incluídos no balanceamento de carga automaticamente. Se estiver  
usando o browser para testar o balanceamento certifique-se de apagar o cookie pois este  
é utilizado para afinidade de sessão \(sticky session\).

### 2.X.7 - Garantia do número de réplicas

![](https://storage.googleapis.com/workshop-openshift/delete-pod.gif)

Remova um dos pods.

Selecione um dos pods, no menu superior direito selecione a opção _Actions_ &gt; _Delete_ e confirme a operação.

Selecione a opção _Overview_ no menu lateral esquerdo e veja que um novo pod será recriado.

TIP: O Openshift garante que o número de pods em execução é igual ao número estipulado, eliminando o risco  
que uma aplicação fique indisponível esperando intervenção humana.

### 2.X.8 - Deploy usando Source to Image \(S2I\)

### 2.X.9 - Criar nova aplicação no github

Usaremos uma aplicação php como exemplo, sinta-se a vontade para usar a sua linguagem de preferência, mas  
tenha em mente que depois conectaremos a um banco de dados e utilizaremos variáveis de ambiente.

Crie um repositório com o nome `workshop-php`

Faça o clone deste novo repositório e crie a página inicial `index.php`

```
git clone https://github.com/<seu-usuario/workshop-php.git
```

Crie o arquivo `index.php` com o seguinte conteúdo

```
<?php
echo "<h1>Openshift Workshop o/</h1> ";
echo $_SERVER['SERVER_ADDR']
?>
```

TIP: Essa linha com o conteudo $\_SERVER é opcional, ela irá mostrar na tela o IP do pod em que está sendo executada.

Faça o commit do código para o servidor git.

```
git add index.php
git commit -am "first commit"
git push -u origin master
```

Agora que já temos uma aplicação, podemos prosseguir.

### 2.X.10 - Deploy utilizando S2I

![](https://storage.googleapis.com/workshop-openshift/s2i-deploy.gif)

* Selecione no menu superior `Add to project`
* Selecione o template `PHP` no submenu `Browser Catalog`.
* Selecione o template `PHP` na versão `7.0`.
* Preencha o campo `Name` com o valor `workshop-php` 
* Preencha o campo `Git Repository URL` com o valor `https://github.com/<seu-usuario>/workshop.php.git`

Acesse a url gerada e verifique a aplicação em funcionamento. O resultado deve ser algo similar a isso:

![](https://storage.googleapis.com/workshop-openshift/s2i-deploy-final.png)

### 2.X.11 - Scale up 4

Através da seta para cima na lateral do círculo do pod, clique até escalar a aplicação para 4 pods.

![](https://storage.googleapis.com/workshop-openshift/scale-up-4.png)

### 2.X.12 - Integração Continua

Para que sempre que ocorra um commit o Openshift faça de forma automátia o processo de build e deploy, iremos configurar  
um webhook, dessa forma o servidor git avisará o Openshift sempre que um commit novo ocorrer.

### 2.X.13 - Configuração webhook

![](https://storage.googleapis.com/workshop-openshift/webhook.gif)

No _Openshift_:

* Selecione `Builds` &gt; `Build`
* Selecione `workshop-php`
* Selecione a aba `Configuration` e clique em copy no campo `Github Webhook URL`

No _Github.com_:

* Selecione `Settings` no menu horizontal
* Selecione o `Webhooks` no menu lateral esquerdo 
* Selecione `Add Webhooks`, cole a URL copiada no campo `Payload URL`, no campo `Content Type` selecione a opção `application/json`
* Finalize no botão `Add webhook`

### 2.X.14 - Altera aplicação

Para fazermos uma alteração na aplicação, vamos inserir a versão na página inicial da aplicação.

No `index.php` insira uma linha com a versão da aplicação.

```
echo "<h4>Versão 2.0</h4> ";
```

### 2.X.15 - Acompanhe o rolling deployment

TIP: Observe que não ocorre indisponibilidade durante o deployment

### 2.X.16 - Log aggregation

Devido a facilidade de criar e escalar aplicações,  
torna-se praticamente impossível rastrear algum erro de forma  
individual procurando em cada container. Para resolver este problema  
o Openshift possui uma solução de agregação de logs que pode ser utilizado  
pela console do Kibana.

* Navegue até a tab de logs de um dos pods.
* Selecione a opção `Archive`

![](https://storage.googleapis.com/workshop-openshift/log-aggregation.png)

É possível criar relatórios e consolidar em dashboards, com informações mostrando o crescimento de erros da aplicação `x` nos últimos meses ou semanas, etc...

### 2.X.17 - Persistindo dados em um banco de dados

### 2.X.18 - Deploy de um MYSQL persistente através de um template

* Selecione no menu super "Add to project"
* Selecione a sub categoria "Data Stores" &gt; "MySQL \(Persistent\) 
* Preencha os campos do template com os seguintes valores:
  * `Database Service Name` com `mysql`
  * `MySQL Connection Username` com `redhat`
  * `MySQL Connection Password` com `redhat@123`
  * `MySQL root user Password` com `redhat@123`
  * `MySQL Database Name com` com `workshop`
  * `Volume Capacity com` com `1Gi`

O resultado deve ser similar a este

![](https://storage.googleapis.com/workshop-openshift/mysql-persistent.png)

TIP: Observe através do menu lateral `Storage` que o volume para persistência dos registros no MySQL foi provisionado dinâmicamente

![](https://storage.googleapis.com/workshop-openshift/mysql-storage.png)

### 2.X.19 - Altere a aplicação para apontar para o banco de dados persistente

Vamos mostrar uma lista de cidades cadastradas no banco de dados com essa aplicação.  
Para isso o primeiro passo será conectar a nossa aplicação já existente neste banco de dados, para isso  
precisamos adicionar o trecho de código abaixo ao arquivo `index.php` já existente.

```
echo "<br><hr>";
echo "<h2>Cidades cadastradas no Banco de Dados:</h2>";
$conn = new mysqli("mysql", "redhat", "redhat@123", "workshop");
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}
$result = $conn->query("SELECT nome FROM cidade");
if ($result->num_rows > 0) {
    while($row = $result->fetch_assoc()) {
        echo "<h3>" . $row["nome"] . "</h3>";
    }
} else {
    echo "0 results";
}
$conn->close();
?>
```

Como a tabela que está sendo consultada ainda não existe você estará vendo que existem zero cidades cadastradas neste momento.

![](https://storage.googleapis.com/workshop-openshift/app-zero-result.png)

### 2.X.20 - Popule o banco de dados a partir da sua máquina local

Para criar a nossa tabela que a nossa aplicação está consumindo os dados, vamos utilizar o recurso de port-forward. Este  
recurso permite que uma porta TCP remota possa ser acessada como se estivesse disponível localmente  
através do uso de túnels.

```
oc login https://console.ocp.rhbrlab.com:8443 -u <user>
oc get pods 
oc port-forward <pod id> 3306:3306
```

![](https://storage.googleapis.com/workshop-openshift/port-forward.png)

Neste momento temos o MYSQL disponível "localmente", podemos conectar a ele com ferramentas gráficas ou como será demonstrado  
aqui com o mysql client.

```
mysql -u redhat -h 127.0.0.1 -p

USE workshop;
CREATE TABLE cidade (id INT NOT NULL, nome VARCHAR(50) NOT NULL, PRIMARY KEY (id));
INSERT INTO cidade (id,nome) VALUES(1,"Rio de Janeiro");
INSERT INTO cidade (id,nome) VALUES(2,"Brasilia");
INSERT INTO cidade (id,nome) VALUES(3,"Recife");
SELECT * FROM cidade;
```

Ao acessar novamente a interface de nossas aplicação a mesma deverá estar mostrando a lista de cidades incluídas neste passo.

![](https://storage.googleapis.com/workshop-openshift/app-with-results.png)

### 2.X.21 - Pipeline

O Openshift possui integração nativa com o Jenkins, o que nos permite criar pipelines de forma  
simples.

Com o objetivo é utilizar o pipeline, devemos desabilitar  
o deploy automático nas configurações do `DeploymentConfig`.

![](https://storage.googleapis.com/workshop-openshift/disable-deploy.png)

Para isso, precisamos criar um `BuildConfig`. Dentro do seu repositório do `workshop-php`, crie o  
diretório pipeline.

```
mkdir pipeline
```

Crie o arquivo `buildconfig.yaml`

```
kind: "BuildConfig"
apiVersion: "v1"
metadata:
  name: "workshop-pipeline"
  annotations:
    pipeline.alpha.openshift.io/uses: '[{"name": "workshop-php", "kind": "DeploymentConfig"}]'
spec:
  source:
    type: "Git"
    git:
      uri: "http://github.com/<seu-usuario>/workshop-php.git"
  strategy:
    type: "JenkinsPipeline"
    jenkinsPipelineStrategy:
      jenkinsfilePath: "pipeline/jenkins-pipeline.groovy"
```

Vamos definir um pipeline simples, crie o arquivo  
jenkins-pipeline.groovy

```
node('maven') {
    stage('build') {
        echo 'building app :)'
        openshiftBuild(buildConfig: 'workshop-php', showBuildLogs: 'true')
    }
    stage('verify') {
        echo 'dummy verification....'
    }
    stage('deploy') {
        input 'Manual Approval'
        openshiftDeploy(deploymentConfig: 'workshop-php')
    }
}
```

Pela linha de comando, crie o build config que definimos no passo anterior:

`oc create -f buildconfig.yaml`

Agora no menu lateral esquerdo, selecione a opção `Builds` &gt; `Pipelines` e  
selecione a opção `Start pipeline`

![](https://storage.googleapis.com/workshop-openshift/start-pipeline.png)

### 2.X.22 - Extras

* Rsync 
* Health Check
* Resource limits 
* Auto Scale 
* Rollback 
* Deployment
* Canary release 
* Blue Green Deployment 



