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
  --use-existing-config
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
  --use-existing-config
```

Nessa versão do cluster up existe um bug nas métricas. Para corrigi-lo, crie um playbook:

```
cat <<EOF > fix.yml
- name: Fix Metrics
  hosts: 127.0.0.1
  connection: local
  tasks:
    - name: OpenShift Login
      shell: oc login -u system:admin --insecure-skip-tls-verify
      
    - name: Get Metrics Error Pod
      shell: oc get pods -n openshift-infra | grep Error | head -n1 | cut -d' ' -f1
      register: metrics_pod
      until: metrics_pod.stdout != ""
      retries: 20
      delay: 30

    - name: Fix Metrics Deployment
      shell: oc debug {{ metrics_pod.stdout }} -n openshift-infra -- /usr/bin/bash -c "sed -i 's/- include: validate_hostnames.yml/#- include: validate_hostnames.yml/' /usr/share/ansible/openshift-ansible/playbooks/common/openshift-cluster/std_include.yml && ansible-playbook -i /tmp/inventory playbooks/byo/openshift-cluster/openshift-metrics.yml"
EOF
```

E execute-o:

```
ansible-playbook fix.yml
```

#### 2.1.1.1.1 Acessando a Web Console

Se os passos anteriores foram executados com sucesso, você terá uma tela com a seguinte informação:

![](/assets/Selection_226.png)

1. Esse é a url de acesso para a Web Console
2. Suas credenciais para acesso ao Openshift
3. Usuário com privilégio elevado para tarefas administrativas do cluster



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

