### Binary Deployment

O Openshift permite que imagens docker sejam construídas automaticamente, informando somente o repositório do código-fonte por meio do Source-to-Image como você pode testar no Lab 2.1.5. Mas existem casos que você já tem o binário da sua aplicação compilado e pronto em um repositório como o Nexus. O Openshift também possibilita que possamos executar o processo do source-to-image utilizando esse binário.

Iremos criar um tomcat com um aplicação chamada contador.

#### Preparando o ambiente

Vamos criar agora uma pasta para trabahar nessa demonstração:

```
mkdir -p ~/binary-deployment/deployments && cd ~/binary-deployment
```

Para testar essa funcionalidade, vamos baixar o binário da nossa aplicação de exemplo. Clique [nesse link](https://github.com/luszczynski/contador/blob/master/contador.war?raw=true) para iniciar o download e salve na pasta `~/binary-deployment/deployments`. Ou execute o seguinte comando:

```
curl https://github.com/luszczynski/contador/blob/master/contador.war?raw=true -o ~/binary-deployment/deployments/contador.war
```

![](/assets/show-contador.gif)

#### Criando binary deployment no Openshift

Agora precisamos falar para o Openshift criar um novo build usando o tomcat e dizendo para ele para não usar o código-fonte e sim o binário da aplicação.

```
oc new-build --image-stream=jboss-webserver30-tomcat8-openshift --binary=true --name=binary-deployment -n <nome do seu projeto>
```

Esse comando irá criar um BuildConfig que nada mais é que um arquivo descritor explicando como o Openshift deve construir a imagem docker. O detalhe nesse caso é o parametro **--binary=true. **Ele instrui que o BuildConfig use o binário ao invés do código-fonte da aplicação.

![](/assets/bc-binary.gif)Se olharmos os BuildConfig que acabamos de criar, podemos perceber que ele é do tipo binário. Para ver os buildconfigs executamos:

```
oc get bc -n <nome do seu projeto>
```

![](/assets/Selection_057.png)

Nosso próximo passo é executar o build que acabamos de criar:

```
oc start-build binary-deployment --from-dir=. -n <nome do seu projeto>
```

Estamos passando nesse comando qual o diretório que queremos enviar para a imagem do Tomcat. Nesse caso, é o diretório atual. A imagem do Tomcat sabe que deve pegar os arquivos que estão dentro da pasta **deployment** e jogar na pasta do Tomcat responsável pelo deployment.

Isso tudo acontece porque essa imagem do Tomcat usa S2I e portanto sabe o que fazer quando recebe um binário. Você poderia criar uma imagem e adicionar esse comportamento caso desejado.

![](/assets/start-build.gif)

Após executar o comando acima, um novo build é iniciado. Para visualizar, acesse:

1. No menu lateral, clique em **Builds** -&gt; **Builds**
2. Na tabela seguinte, clique em **binary-deployment**

![](/assets/access-build.gif)Assim que o build concluir, ele irá apresentar o status como **completed**

![](/assets/Selection_058.png)Agora podemos criar nossa aplicação com base na nova imagem gerado por esse build.

Para isso, executamos:

```
oc new-app binary-deployment -n <nome do seu projeto>
```

![](/assets/new-app-binary-deployment.gif)Preciamos por último criar uma rota para que nossa aplicação possa ser acessada por fora do Openshift.

```
oc expose svc binary-deployment -n <nome do seu projeto>
```

No final, sua aplicação estará disponível no cluster da seguinte forma:

![](/assets/Selection_059.png)

