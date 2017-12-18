### Deploy imagem do Docker Hub

![](https://storage.googleapis.com/workshop-openshift/deploy-docker-image.gif)

#### Escolha a imagem

Você pode usar a imagem criada durante o lab de introdução ao Docker. Ela ficou salva no seguinte formato

```
docker.io/<usuario>/workshop-openshift
```

Caso não tenha nenhuma você pode usar essa de exemplo:

[https://hub.docker.com/r/davivcgarcia/workshop-openshift/](https://hub.docker.com/r/davivcgarcia/workshop-openshift/)

Ficando assim o formato:

```
docker.io/davivcgarcia/workshop-openshift
```

> **OBS: Por questões de segurança a imagem não pode ser executada utilizando o usuário root.**

Se a imagem escolhida rodar como root, o Openshift te avisa na console \(por meio de uma tarja laranja\) que ela pode eventualmente não executar conforme o esperado.

![](/assets/img-root.gif)

Caso queira usar a linha de comando, execute:

`oc new-app <nome do seu usuario>/workshop-openshift -n <nome do seu projeto do openshift>`

![](/assets/Peek 2017-12-07 09-29.gif)

#### Crie a rota para expor a aplicação externamente

Na interface web selecione a opção _**create route.**_

Command line

`oc expose svc workshop-openshift`

![](/assets/svc.gif)

#### Explorando a GUI do POD

![](https://storage.googleapis.com/workshop-openshift/pod-navigation.gif)

Selecione o pod e navegue entre as abas: `Details, Environment, Metrics, Logs, Terminal e Events`

Mais informações:[ ](https://blog.openshift.com/deploying-images-from-dockerhub/)

[https://blog.openshift.com/getting-any-docker-image-running-in-your-own-openshift-cluster/](https://blog.openshift.com/getting-any-docker-image-running-in-your-own-openshift-cluster/)

[https://blog.openshift.com/deploying-images-from-dockerhub/](https://blog.openshift.com/deploying-images-from-dockerhub/)

