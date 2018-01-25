### Canary Release

Canary release é uma técnica utilizada para reduzir o risco de introduzir uma nova versão de software em ambiente de produção, lançando lentamente a mudança para um pequeno grupo de usuários antes de lançá-lo para toda a infra-estrutura e disponibilizá-lo para todos.

![](/assets/canary-release-2.png)

#### Preparando nossa aplicação

Vamos lançar uma nova versão da nossa aplicação e aplicar a técnica de Canary Release. Para isso, vamos criar um branch no git contendo nosso código mais novo.

Na raiz do seu repositório git, execute:

```
git branch v3.0
git checkout v3.0
```

![](/assets/git-branch.gif)

Agora vamos editar o arquivo e alterar a versão da nossa aplicação para 3.0 conforme abaixo:

```
<?php
echo "<h1>Openshift Workshop v3.0</h1> ";
echo $_SERVER['SERVER_ADDR']
?>
```

![](/assets/change-version.gif)

Quando finalizado, podemos agora fazer o commit e push para nosso repositório.

```
git add index.php
git commit -m "v3.0"
git push origin v3.0
```

Se fizemos tudo certo, em nosso Github deve existir um novo branch:

#### ![](/assets/show-branch.gif)Criando nova versão no Openshift

Precisamos criar uma nova versão da nossa aplicação usando o branch v3.0.

Selecione no menu superior `Add to project`

* Selecione o template `PHP` no submenu `Browser Catalog`.
* Selecione o template `PHP` na versão `7.0`.
* Preencha o campo `Name` com o valor `workshop-php-v3` 
* Preencha o campo `Git Repository URL` com o valor `https://github.com/<seu-usuario>/workshop-php.git`
* Clique em `Show advanced options`
* Preencha o campo `Git Reference` com o valor **v3.0**
* Desça a página toda e clique em `Create`

![](/assets/choose-v3.gif)Quando tudo finalizar, teremos 2 versões da nossa aplicação rodando no Openshift.

![](/assets/Selection_048.png)Se abrirmos o link da primeira versão temos:

![](/assets/Selection_049.png)

E se abrirmos o link da última versão que criamos:

![](/assets/Selection_050.png)

A URL de acesso da primeira versão é a única que nossos usuários conhecem e portanto é nela que iremos fazer a separação da quantidade de acesso.

![](/assets/Selection_051.png)

Vamos configurar para que a versão 3.0 tenha somente **10%** dos acessos enquanto a versão 1.0 terá **90%.**

* Clique em **Applications** -&gt; **Routes**
* Na tabela, seleciona a rota de nome **workshop-php**
* No menu superior direito clique em **Actions** -&gt; **Edit**
* Selecione o campo **Split traffic across multiple services**
* Arraste a barra para que o fique somente 10% para o **workshop-php-v3**

![](/assets/select-route.gif)

E altere os valores conforme figura abaixo:

![](/assets/Selection_052.png)Assim que salvarmos, o Openshift irá mostrar uma tela com as configurações que escolhemos.

![](/assets/Selection_053.png)

E também na tela inicial temos um aviso que o acesso está sendo divido.

#### ![](/assets/Selection_054.png)

#### Testando a divisão de acesso na nossa aplicação

Para testarmos que realmente 90% do acesso está indo para versão 1.0 e 10% para v3.0, vamos usar um comando do shell:

```bash
while [ true ]; do curl http://workshop-php-testdrive.apps.ocp.rhbrlab.com/; sleep 1.3; echo; done
```

Esse comando irá executar um curl na sua aplicaçao em cada 1s.

Altere a url acima de acordo com a sua aplicação.

Perceba que a cada 10 requisições para nossa aplicação, 1 é enviada para a versão 3.0.

![](/assets/Selection_055.png)

