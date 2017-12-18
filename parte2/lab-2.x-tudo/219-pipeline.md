### Pipeline

O Openshift possui integração nativa com o Jenkins, o que nos permite criar pipelines de forma simples.

Com o objetivo é utilizar o pipeline, devemos desabilitar o deploy automático nas configurações do `DeploymentConfig`.

![](https://storage.googleapis.com/workshop-openshift/disable-deploy.png)

Para isso, precisamos criar um `BuildConfig`. Dentro do seu repositório do `workshop-php`, crie o  
diretório pipeline.

```
mkdir pipeline
```

Crie o arquivo `buildconfig.yaml Repare que existe um campo que deve ser alterado com o nome do usuário do github.`

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
      uri: "http://github.com/<seu-usuario-do-github>/workshop-php.git"
  strategy:
    type: "JenkinsPipeline"
    jenkinsPipelineStrategy:
      jenkinsfilePath: "pipeline/jenkins-pipeline.groovy"
```

Vamos definir um pipeline simples, crie o arquivo `jenkins-pipeline.groovy`

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
    stage('promoting to QA') {
       echo 'fake stage...'
       sleep 5 
    }
}
```

Pela linha de comando, crie o build config que definimos no passo anterior:

`oc create -f buildconfig.yaml`

> Observe que logo ao fim da execução deste passo, o Jenkins \(master/slave\) será provisionado automaticamente no projeto em questão.

No menu lateral esquerdo, selecione a opção `Builds` &gt; `Pipelines` e selecione a opção `Start pipeline`

![](https://storage.googleapis.com/workshop-openshift/start-pipeline.png)

### Mais informações

[https://docs.openshift.com/container-platform/3.6/install\_config/configuring\_pipeline\_execution.html](https://docs.openshift.com/container-platform/3.6/install_config/configuring_pipeline_execution.html)

[https://docs.openshift.com/container-platform/3.6/using\_images/other\_images/jenkins.html](https://docs.openshift.com/container-platform/3.6/using_images/other_images/jenkins.html)

[https://docs.openshift.com/container-platform/3.6/dev\_guide/application\_lifecycle/promoting\_applications.html](https://docs.openshift.com/container-platform/3.6/dev_guide/application_lifecycle/promoting_applications.html)

