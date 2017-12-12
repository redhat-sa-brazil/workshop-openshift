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

![](/assets/show-contador.gif)Agora precisamos falar para o Openshift criar um novo build usando o tomcat e dizendo para ele para não usar o código-fonte e sim o binário da aplicação.

```
oc new-build --image-stream=jboss-webserver30-tomcat8-openshift --binary=true --name=binary-deployment -n <nome do seu projeto>
```

Esse comando irá criar um BuildConfig que nada mais é que um arquivo descritor explicando como o Openshift deve construir a imagem docker. O detalhe nesse caso é o parametro **--binary=true. **Ele instrui que o BuildConfig use o binário ao invés do código-fonte da aplicação.



