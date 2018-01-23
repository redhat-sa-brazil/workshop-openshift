### Acesso ao ambiente OpenShift

![](https://storage.googleapis.com/workshop-openshift/oc-login.gif)

1. Acesse a url: [https://console.paas.rhbrlab.com/console/](https://console.ocp.rhbrlab.com:8443/console/)
2. Faça o login através da opção **Red Hat Single Sign ON**
  * informe as credenciais de acordo com o login designado pelo instrutor
  * altere sua senha no primeiro login 
3. No menu superior direito clique no ícone de ajuda e selecione a opção "**Command Line Tools**"
4. Copie o comando gerado "`oc login..`.". \(clique no botão no final do campo\) O seu token de acesso já estará nessa string.
5. Cole a linha de comando no seu terminal conforme exemplo abaixo

```
oc login https://console.paas.rhbrlab.com --token=fkjaflowruwwoeuwourwori....................
```

**No fim do procedimento deverá aparecer a mensagem "Login success".**

Neste momento você já estará dentro do seu projeto. Para listar os PODs deste projeto você pode utilizar

`oc get pods`

Também é possível visualizar quais projetos você tem permissão de acesso:

```
oc get projects
```

![](/assets/oc-get-projects.gif)

