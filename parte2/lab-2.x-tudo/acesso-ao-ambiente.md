### Acesso ao ambiente OpenShift

![](https://storage.googleapis.com/workshop-openshift/oc-login.gif)

1. Acesse a url: [https://console.paas.rhbrlab.com/console/](https://console.paas.rhbrlab.com/console/)
2. Faça o login através da opção **Red Hat Single Sign ON**

![](/assets/Selection_207.png)

1. * informe as credenciais de acordo com o login designado pelo instrutor
   * altere sua senha no primeiro login 

3. No menu superior direito clique no ícone de ajuda e selecione a opção "**Command Line Tools**"



4. Copie o comando gerado "`oc login..`.". \(clique no botão no final do campo\) O seu token de acesso já estará nessa string.

5. Cole a linha de comando no seu terminal conforme exemplo abaixo

```
oc login https://console.paas.rhbrlab.com --token=fkjaflowruwwoeuwourwori....................
```



**No fim do procedimento deverá aparecer a mensagem "Login success".**

Neste momento você já estará dentro do seu projeto.

A sua tela será semelhante a essa:

![](/assets/Selection_202.png)Esse nome destacado na imagem acima, é o `Display Name`do seu projeto. Na prática é um nome mais amigável.

Precisaremos usar o nome do seu projeto \(que não é o display name\) para várias operações nos labs posteriores. Para descobrir esse nome, basta ver um pequeno nome abaixo do display name conforme mostra a imagem abaixo:

![](/assets/Selection_203.png)O nome do seu projeto também pode ser visto pela linha de comando:

```
oc get projects
```

![](/assets/oc-get-projects.gif)

Se você precisar ver os dados do seu projeto, basta clicar no menu de projetos conforme imagem abaixo:

![](/assets/Selection_204.png)

