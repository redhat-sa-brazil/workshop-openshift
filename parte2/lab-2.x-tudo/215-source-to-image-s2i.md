### Deploy usando Source to Image \(S2I\)

#### Criar nova aplicação no github

Usaremos uma aplicação php como exemplo, sinta-se a vontade para usar a sua linguagem de preferência, mas  
tenha em mente que depois conectaremos a um banco de dados e utilizaremos variáveis de ambiente.

Crie um repositório com o nome `workshop-php`

Faça o clone deste novo repositório e crie a página inicial `index.php`

```
git clone https://github.com/<seu-usuario>/workshop-php.git && cd workshop-php
```

Crie o arquivo `index.php` com o seguinte conteúdo

```
<?php
echo "<h1>Openshift Workshop v1.0</h1> ";
echo $_SERVER['SERVER_ADDR']
?>
```

> Essa linha com o conteudo $\_SERVER é opcional, ela irá mostrar na tela o IP do pod em que está sendo executada.

Faça o commit do código para o servidor git.

```
git add index.php
git commit -am "first commit"
git push -u origin master
```

Agora que já temos uma aplicação, podemos prosseguir.

#### Deploy utilizando S2I

![](https://storage.googleapis.com/workshop-openshift/s2i-deploy.gif)

* Selecione no menu superior `Add to project`
* Selecione o template `PHP` no submenu `Browser Catalog`.
* Selecione o template `PHP` na versão `7.0`.
* Preencha o campo `Name` com o valor `workshop-php` 
* Preencha o campo `Git Repository URL` com o valor `https://github.com/<seu-usuario>/workshop.php.git`

Acesse a url gerada e verifique a aplicação em funcionamento. O resultado deve ser algo similar a isso:

![](https://storage.googleapis.com/workshop-openshift/s2i-deploy-final.png)

Você também pode usar a linha de comando para fazer o S2I.

```
oc new-app https://github.com/<seu-usuario>/workshop.php.git -n <nome do seu projeto do openshift>
```

Nesse caso, o Openshfit irá tentar adivinhar qual a linguagem que você utilizou na sua aplicação.

#### Escalar para 4 PODs

Através da seta para cima na lateral do círculo do pod, clique até escalar a aplicação para 4 pods.

#### ![](https://storage.googleapis.com/workshop-openshift/scale-up-4.png)

#### Source-to-Image com outras imagens

Iremos agora utilizar o S2I com um template do Apache HTTPD. Já existe [um repositório](https://github.com/openshift/httpd-ex.git) com um arquivo de exemplo para testarmos essa funcionalidade.

1. No menu superior clique em **Add to project**
2. Na busca, digite **httpd**
3. Selecione o template **Httpd** versão **2.4**

![](/assets/Selection_060.png)Logo em seguida, preencha os valores conforme abaixo:

* Name: **apache**
* Git Repository Url: Clique no botão **try it**

![](/assets/select-apache.gif)Caso sua aplicação não abra e mostre a seguinte tela:

![](/assets/Selection_061.png)Isso pode ser devido a um bug no template do Openshift. Para corrigir, basta alterar a porta que a nossa route está utilizando.

Se olharmos a nossa rota, ela está direcionando o acesso para a porta 80.

![](/assets/Selection_062.png)Quando abrimos o serviço, percebemos que nosso container utiliza também outras portas:

![](/assets/Selection_063.png)Nosso apache está escutando na porta 8080 e não na 80.

Vamos alterar a rota para apontar para essa porta. Primeiro abrimos a rota do Apache.

![](/assets/route.gif)Logo em seguida, clicamos no menu lateral direito **Action** -&gt; **Edit**

E trocamos a porta que nossa rota está utilizando para a **8080**

![](/assets/altera-porta.gif)

Agora, nossa aplicação já deve estar disponível.

![](/assets/Selection_064.png)

##### Mais informações:

[https://docs.openshift.com/container-platform/3.6/using\_images/s2i\_images/index.html](https://docs.openshift.com/container-platform/3.6/using_images/s2i_images/index.html)

[https://docs.openshift.com/container-platform/3.6/creating\_images/s2i.html](https://docs.openshift.com/container-platform/3.6/creating_images/s2i.html)

### 



