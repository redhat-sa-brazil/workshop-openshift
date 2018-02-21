### Deploy imagem do Docker Hub

Vamos agora implantar uma imagem existente no Docker Hub. Para executar a imagem. siga os passos abaixo:

**Openshift 3.7**

![](/assets/deploy-image-docker-hub.gif)

#### Escolha a imagem

Você pode usar a imagem criada durante o lab de introdução ao Docker. Ela ficou salva no seguinte formato

```
docker.io/<usuario do dockerhub>/workshop-openshift
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

`oc new-app <nome do seu usuario docker.io>/workshop-openshift -n <nome do seu projeto do openshift>`

![](/assets/Peek 2017-12-07 09-29.gif)

#### Crie a rota para expor a aplicação externamente

Na interface web selecione a opção _**create route.**_

![](/assets/Selection_227.png)E depois clique em **create**

![](/assets/Selection_228.png)Depois de criado, a url irá aparece na tela principal

![](/assets/Selection_229.png)

Command line

Também podemos usar a linha de comando para criar a nossa rota. Para isso, basta executar:

`oc expose svc workshop-openshift -n <nome do seu projeto do openshift>`

![](/assets/svc.gif)

#### Explorando a GUI do POD

Para ver detalhes do container que acabamos de criar, basta clicar em cima do circulo azul e depois navegar pelas abas `Details, Environment, Metrics, Logs, Terminal e Events`

![](/assets/overview.gif)

Detalhes do POD![](/assets/Selection_230.png)

1. Ip do POD
2. Node no qual o POD está executando
3. Imagem utilizada
4. Porta exposta pelo POD

Environment

![](/assets/Selection_234.png)

Logs do POD

![](/assets/Selection_231.png)

Terminal do POD

![](/assets/Selection_232.png)

Eventos do POD

![](/assets/Selection_233.png)

Mais informações:[ ](https://blog.openshift.com/deploying-images-from-dockerhub/)

[https://blog.openshift.com/getting-any-docker-image-running-in-your-own-openshift-cluster/](https://blog.openshift.com/getting-any-docker-image-running-in-your-own-openshift-cluster/)

[https://blog.openshift.com/deploying-images-from-dockerhub/](https://blog.openshift.com/deploying-images-from-dockerhub/)

