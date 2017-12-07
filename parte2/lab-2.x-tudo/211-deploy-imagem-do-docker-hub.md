### Deploy imagem do Docker Hub

![](https://storage.googleapis.com/workshop-openshift/deploy-docker-image.gif)

#### Escolha a imagem

Você pode usar a imagem criada durante o lab de introdução ao Docker. Ela ficou salva no seguinte formato

```
docker.io/<usuario>/workshop-openshift
```

Caso não tenha nenhuma você pode usar essa de exemplo:

[https://hub.docker.com/r/davivcgarcia/workshop-openshift/](https://hub.docker.com/r/davivcgarcia/workshop-openshift/)

> **OBS: Por questões de segurança a imagem não pode ser executada utilizando o usuário root.**

Command line

`oc new-app davivcgarcia/workshop-openshift`

#### Crie a rota para expor a aplicação externamente

Na interface web selecione a opção _**create route.**_

Command line

`oc expose svc workshop-openshift`

#### Explorando a GUI do POD

![](https://storage.googleapis.com/workshop-openshift/pod-navigation.gif)

Selecione o pod e navegue entre as abas: `Details, Environment, Metrics, Logs, Terminal e Events`

Mais informações:[ ](https://blog.openshift.com/deploying-images-from-dockerhub/)

[https://blog.openshift.com/getting-any-docker-image-running-in-your-own-openshift-cluster/](https://blog.openshift.com/getting-any-docker-image-running-in-your-own-openshift-cluster/)

[https://blog.openshift.com/deploying-images-from-dockerhub/](https://blog.openshift.com/deploying-images-from-dockerhub/)

