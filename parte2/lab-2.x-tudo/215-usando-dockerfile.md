### Usando Dockerfile

Além do Source to Image, o Openshift permite realiza o build de `Dockerfile` para você. Basta adicionar o seu `Dockerfile`em um repositório git e informar ao Openshift que iremos utilizar a estratégia de build do tipo docker. Para esse exemplo, iremos **utilizar o mesmo repositório criado no lab anterior **conforme exemplo abaixo**:**

```
https://github.com/<seu-usuario>/workshop-php.git
```

#### Criando nosso Dockerfile

Vamos criar um Dockerfile com base na [imagem oficial do PHP para Openshift](https://access.redhat.com/containers/#/registry.access.redhat.com/rhscl/php-70-rhel7). É importante salientar que, existem boas práticas na construção de [imagens Docker](https://docs.openshift.com/container-platform/3.7/creating_images/guidelines.html#general-container-image-guidelines) e também em[ imagens para o Openshift](https://docs.openshift.com/container-platform/3.7/creating_images/guidelines.html#openshift-specific-guidelines).

Abaixo segue o conteúdo do arquivo:

```
FROM registry.access.redhat.com/rhscl/php-70-rhel7

RUN echo "<h1>Meu Dockerfile</h1>" > /opt/app-root/src/index.php

CMD ["container-entrypoint", "/usr/libexec/s2i/run"]
```

Salve esse arquivo com nome de **Dockerfile** na raiz do nosso git e execute:

```
git add Dockerfile
git commit -m "Dockerfile adicionado"
git push
```

#### Executando o Dockerfile com Openshift

Para criar uma aplicação com base no Dockerfile criado, precisamos executar o seguinte comando:

```
oc new-app --name=dockerfile-app --strategy=docker https://github.com/<seu-usuario>/workshop-php.git -n <nome do seu projeto do openshift>
```

O valor default para o parametro **strategy** é **source. **Isso indica que, por padrão, o Openshift irá analisar o repositório git tentando compilar o código da aplicação e usar o source-to-image. No nosso caso, queremos que ele use somente o Dockerfile e ignore o código fonte. Por isso informamos o parametro **--strategy=docker**

Assim que executamos o comando, o Openshift inicia o novo build.

![](/assets/Selection_044.png)A diferença desse build para o source-to-image executando anteriormente, é que nesse caso o Openshift está construindo nossa imagem Docker usando Dockerfile. Se acessarmos o log do build, podemos ver ae execução do nosso código.

![](/assets/Selection_046.png)Para finalizar, crie uma rota no Openshift para podermos acessar nossa aplicação:

```
oc expose svc dockerfile-app -n <nome do seu projeto>
```



