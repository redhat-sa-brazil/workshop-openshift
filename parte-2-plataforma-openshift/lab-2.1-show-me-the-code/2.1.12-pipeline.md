# 2.1.12 - Pipeline

## Pipeline

O Openshift possui integração nativa com o Jenkins, o que nos permite criar pipelines de forma simples.

Com o objetivo é utilizar o pipeline, devemos desabilitar o deploy automático nas configurações do `DeploymentConfig`.

![](https://storage.googleapis.com/workshop-openshift/disable-deploy.png)

Para isso, precisamos criar um `BuildConfig.`

Crie um arquivo chamado `jenkins-pipeline.groovy` dentro do seu repositório do github. Para isso, siga o procedimento, já demonstrado nos labs anteriores, de criação do novo arquivo pela Web Console do Github. O conteúdo do arquivo segue abaixo:

```groovy
 node('maven') {
    stage('build') {
        echo 'building app :)'
        openshiftBuild(buildConfig: 'workshop-ocp', showBuildLogs: 'true')
    }
    stage('verify') {
        echo 'dummy verification....'
    }
    stage('deploy') {
        input 'Manual Approval'
        openshiftDeploy(deploymentConfig: 'workshop-ocp')
    }
    stage('promoting to QA') {
       echo 'fake stage...'
       sleep 5 
    }
}
```

No final, seu repositório deve estar conforme imagem abaixo:

![](../../extras/selection_282.png)

Você também pode fazer essa passo pela linha de comando do git.

Antes de continuar, precisamos fazer push para o repositório do github:

```text
git add .
git commit -m "criado jenkinsfile"
git push origin master
```

Pela console, clique em `Add to Project > Import YAML / JSON` e cole o conteúdo abaixo:

> AVISO: Repare que existe um campo que deve ser alterado com o nome do usuário do github.

```yaml
kind: "BuildConfig"
apiVersion: "v1"
metadata:
  name: "workshop-pipeline"
  annotations:
    pipeline.alpha.openshift.io/uses: '[{"name": "workshop-ocp", "kind": "DeploymentConfig"}]'
spec:
  source:
    type: "Git"
    git:
      uri: "http://github.com/<seu-usuario-do-github>/workshop-ocp.git"
  strategy:
    type: "JenkinsPipeline"
    jenkinsPipelineStrategy:
      jenkinsfilePath: "jenkins-pipeline.groovy"
```

No Openshift 3.7 siga os passos a seguir:

![](../../extras/selection_283.png)

Depois cole o conteúdo do arquivo e altere o nome do usuário do github.

![](../../extras/selection_285.png)

Clique em `Create`

> Observe que logo ao fim da execução deste passo, o Jenkins \(master/slave\) será provisionado automaticamente no projeto em questão.

![](../../extras/selection_287.png)

No menu lateral esquerdo, selecione a opção `Builds` &gt; `Pipelines` e selecione a opção `Start pipeline`

![](../../extras/menu_288.png)

Depois clique em `Start pipeline`

![](../../extras/selection_289.png)

Você pode visualizar o log por meio da opção:

![](../../extras/selection_290.png)

Quando você clicar no log, ele te pedirá para logar usando suas credenciais do Openshift.

![](../../extras/selection_291.png)

Aceite as permissões

![](../../extras/selection_292.png)

Quando seu pipeline estiver executando, ele ficará semelhante a imagem abaixo:

![](../../extras/selection_293.png)

## Limpeza do ambiente

Depois de ter finalizado o seu pipeline, limpe seu ambiente rodando o comando:

```text
oc delete all -l app=jenkins-persistent && oc delete bc workshop-pipeline
```

## Mais informações

[https://docs.openshift.com/container-platform/3.6/install\_config/configuring\_pipeline\_execution.html](https://docs.openshift.com/container-platform/3.6/install_config/configuring_pipeline_execution.html)

[https://docs.openshift.com/container-platform/3.6/using\_images/other\_images/jenkins.html](https://docs.openshift.com/container-platform/3.6/using_images/other_images/jenkins.html)

[https://docs.openshift.com/container-platform/3.6/dev\_guide/application\_lifecycle/promoting\_applications.html](https://docs.openshift.com/container-platform/3.6/dev_guide/application_lifecycle/promoting_applications.html)

