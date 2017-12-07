### Deploy usando Source to Image \(S2I\)

#### Criar nova aplicação no github

Usaremos uma aplicação php como exemplo, sinta-se a vontade para usar a sua linguagem de preferência, mas  
tenha em mente que depois conectaremos a um banco de dados e utilizaremos variáveis de ambiente.

Crie um repositório com o nome `workshop-php`

Faça o clone deste novo repositório e crie a página inicial `index.php`

```
git clone https://github.com/<seu-usuario/workshop-php.git && cd workshop-php 
```

Crie o arquivo `index.php` com o seguinte conteúdo

```
<?php
echo "<h1>Openshift Workshop o/</h1> ";
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

#### Escalar para 4 PODs

Através da seta para cima na lateral do círculo do pod, clique até escalar a aplicação para 4 pods.

![](https://storage.googleapis.com/workshop-openshift/scale-up-4.png)

##### Mais informações:

[https://docs.openshift.com/container-platform/3.6/using\_images/s2i\_images/index.html](https://docs.openshift.com/container-platform/3.6/using_images/s2i_images/index.html)

[https://docs.openshift.com/container-platform/3.6/creating\_images/s2i.html](https://docs.openshift.com/container-platform/3.6/creating_images/s2i.html)

