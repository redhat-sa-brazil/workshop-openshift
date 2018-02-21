### 2.1.1.1 Acesso ao ambiente Openshift Local

Siga os passos abaixo caso o instrutor te solicite uma instalação local do Openshift na sua VM.

* Garanta que os pacotes necessários estão instalados

```
yum install centos-release-openshift-origin origin-clients git ansible -y
```

* Executem o comando abaixo:

```
oc cluster up \
  --public-hostname=<seu ip público> \
  --host-data-dir=/var/lib/origin/openshift.local.etcd \
  --host-config-dir=/var/lib/origin/openshift.local.config \
  --host-pv-dir=/var/lib/origin/openshift.local.pv \
  --metrics \
  --logging
```

Altera o valor do parametro `--public-hostname` para o seu ip público caso esteja executando sua VM na Cloud.

> Você deve ter recebido seu ip público por email no ínicio desse test drive. Caso não consiga achar, entre em contato com seu instrutor.

Se o comando acima falhar com o seguinte erro:

![](/assets/Selection_224.png)Altere o arquivo `/etc/sysconfig/docker` e adicione  `--insecure-registry 172.30.0.0/16` no fim da linha `OPTIONS=` conforme mostra imagem abaixo:

![](/assets/Selection_225.png)

Ou se preferir, rode o comando abaixo:

```
sed -i 's/--signature-verification=false/--signature-verification=false --insecure-registry 172.30.0.0\/16/' /etc/sysconfig/docker
```

Reinicie o docker

```
systemctl restart docker
```

E rode novamente o comando `oc cluster up`

```
oc cluster up \
  --public-hostname=<seu ip público> \
  --host-data-dir=/var/lib/origin/openshift.local.etcd \
  --host-config-dir=/var/lib/origin/openshift.local.config \
  --host-pv-dir=/var/lib/origin/openshift.local.pv \
  --metrics \
  --logging
```





### 2.1.1.2 Acesso ao ambiente OpenShift Nuvem

1. Acesse a url: [https://console.paas.rhbrlab.com/console/](https://console.paas.rhbrlab.com/console/)

2. Faça o login através da opção **Red Hat Single Sign ON**

![](/assets/Selection_207.png)

1. * informe as credenciais de acordo com o login designado pelo instrutor
   * altere sua senha no primeiro login 
2. No menu superior direito clique no ícone de ajuda e selecione a opção "**Command Line Tools**"

3. Copie o comando gerado "`oc login..`.". \(clique no botão no final do campo\) O seu token de acesso já estará nessa string.

4. Cole a linha de comando no seu terminal conforme exemplo abaixo

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

