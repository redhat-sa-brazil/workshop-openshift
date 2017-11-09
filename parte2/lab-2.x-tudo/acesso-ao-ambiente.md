### Acesso ao ambiente OpenShift

![](https://storage.googleapis.com/workshop-openshift/oc-login.gif)



1. Acesse a url: https://console.ocp.rhbrlab.com:8443/console/
2. Insira suas credenciais de acesso.
3. No menu superior direito selecione a opção "**Command Line Tools**"
4. Copie o comando gerado "`oc login..`.". O seu token de acesso já estará nessa string.
5. Cole a linha de comando no seu terminal

**No fim do procedimento deverá aparecer a mensagem "Login success".**

Neste momento você já estará dentro do seu projeto. Para listar os PODs deste projeto você pode utilizar

`oc get pods`



