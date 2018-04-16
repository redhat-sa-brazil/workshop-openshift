# 2.1.5 - Source to Image \(S2I\)

## Criar nova aplicação no github

Usaremos uma aplicação php como exemplo, sinta-se à vontade para usar a sua linguagem de preferência, mas  
tenha em mente que depois conectaremos a um banco de dados e utilizaremos variáveis de ambiente.

Crie um repositório no github com o nome `workshop-ocp`

![](../../extras/selection_237.png)

Depois informe o nome do repositorio:

![](../../extras/selection_239.png)

Crie o arquivo `index.php` com o seguinte conteúdo

```php
<?php
echo "<h1>Openshift Workshop v1.0</h1> ";
echo $_SERVER['SERVER_ADDR'];
?>
```

> Essa linha com o conteudo $\_SERVER é opcional, ela irá mostrar na tela o IP do pod em que está sendo executada.

![](../../extras/selection_240.png)

Conteúdo do arquivo.

![](../../extras/selection_241.png)

Clique em `commit new file` para criar o arquivo.

![](../../extras/selection_242.png)

Os passos mostrados acima também podem ser feitos pela linha de comando conforme abaixo:

Faça o clone deste novo repositório e crie a página inicial `index.php`

```text
git clone https://github.com/<seu-usuario>/workshop-ocp.git && cd workshop-ocp
```

Faça o commit do código para o servidor git.

```bash
git add index.php
git commit -am "first commit"
git push -u origin master
```

No final de tudo, devemos ter um arquivo `index.php` no nosso repositório do github.

![](../../extras/selection_243.png)

Agora que já temos uma aplicação, podemos prosseguir.

## Deploy utilizando S2I

Browse Catalog

![](../../extras/selection_245.png)

Seleciona PHP

![](../../extras/selection_246.png)

![](../../extras/s2i-parte2.gif)

* Selecione no menu superior `Add to project`
* Selecione o template `PHP` no submenu `Browser Catalog`.
* Selecione o template `PHP` na versão `7.0`.
* Preencha o campo `Name` com o valor `workshop-ocp` 
* Preencha o campo `Git Repository URL` com o valor `https://github.com/<seu-usuario-do-github>/workshop-ocp.git`

Um novo build será executado assim que for clicado em `Create`

![](../../extras/selection_298.png)

Caso você encontre o erro abaixo durante o build:

![](../../extras/captura-de-tela-de-2018-02-22-14-15-01.png)

Instale o pacote abaixo:

```text
yum install python-rhsm-certificates -y
```

E execute novamente o build clicando em

1. `Builds` -&gt; `Builds`
2. Clique em `Workshop ocp`
3. No canto direito clique em `Start Build`

Assim que finalizado o build, acesse a url gerada e verifique a aplicação em funcionamento. O resultado deve ser algo similar a isso:

![](../../extras/selection_248.png)

Você também pode usar a linha de comando para fazer o S2I.

```text
oc new-app https://github.com/<seu-usuario>/workshop-ocp.git -n <nome do seu projeto do openshift>
```

Nesse caso, o Openshfit irá tentar adivinhar qual a linguagem que você utilizou na sua aplicação.

## Escalar para 4 PODs

Através da seta para cima na lateral do círculo do pod, clique até escalar a aplicação para 4 pods.

![](../../extras/scale-4.gif)

## Source-to-Image com outras imagens \(Opcional\)

Iremos agora utilizar o S2I com um template do Apache HTTPD. Já existe [um repositório](https://github.com/openshift/httpd-ex.git) com um arquivo de exemplo para testarmos essa funcionalidade.

1. No menu superior clique em **Add to project**
2. Na busca, digite **httpd**
3. Selecione o template **Httpd** versão **2.4**

![](../../extras/selection_060.png)

Logo em seguida, preencha os valores conforme abaixo:

* Name: **apache**
* Git Repository Url: Clique no botão **try it**

![](../../extras/select-apache.gif)

Caso sua aplicação não abra e mostre a seguinte tela:

![](../../extras/selection_061.png)

Isso pode ser devido a um bug no template do Openshift. Para corrigir, basta alterar a porta que a nossa route está utilizando.

Se olharmos a nossa rota, ela está direcionando o acesso para a porta 80.

![](../../extras/selection_062.png)

Quando abrimos o serviço, percebemos que nosso container utiliza também outras portas:

![](../../extras/selection_063.png)

Nosso apache está escutando na porta 8080 e não na 80.

Vamos alterar a rota para apontar para essa porta. Primeiro abrimos a rota do Apache.

![](../../extras/route.gif)

Logo em seguida, clicamos no menu lateral direito **Action** -&gt; **Edit**

E trocamos a porta que nossa rota está utilizando para a **8080**

![](../../extras/altera-porta.gif)

Agora, nossa aplicação já deve estar disponível.

![](../../extras/selection_064.png)

Para limpar nosso ambiente, execute o seguinte comando:

```text
oc delete all -l app=apache -n <nome do seu projeto no openshift>
```

### Mais informações:

[https://docs.openshift.com/container-platform/3.6/using\_images/s2i\_images/index.html](https://docs.openshift.com/container-platform/3.6/using_images/s2i_images/index.html)

[https://docs.openshift.com/container-platform/3.6/creating\_images/s2i.html](https://docs.openshift.com/container-platform/3.6/creating_images/s2i.html)

