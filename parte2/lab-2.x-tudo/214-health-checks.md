### Health Checks

Componentes de software ficam indisponíveis por varias razões, como por exemplo falha de comunicação, erro de configuração ou problemas com dependências externas como banco de dados ou broker de mensagens. O Openshift possui dois recursos bastante poderosos para fazer o health checks de aplicações. O primeiro é que iremos abordar é o Liveness e em seguida o Readiness.

#### Liveness

O liveness verifica se o container ainda está em execução \(de forma sadia\). Se a verificação falhar este container é morto e sujeitado a política de restart que por padrão é "always". Logo o comportamento padrão é se acontecer alguma falha o container é reiniciado.

O liveness pode ser verificado de 3 possíveis formas:

* Executando um handshake de portas
* Executando alguns dos verbos HTTP \(GET, POST, PUT, DELETE, etc\) em um contexto da aplicação
* Executando um comando ou script dentro do container

#### Readiness

O readiness define quando que o container está pronto para receber requisições. Caso a verificação do readiness falhe nenhuma requisição será direcionado para este container até que a verificação seja satisfeita.

#### Configuração no Openshift

![](https://storage.googleapis.com/workshop-openshift/ocp-health-checks.gif)

1. Selecione no menu vertical esquerdo a opção **Deployments &gt; openshift-workshop**
2. Selecione **Actions &gt; Edit Health Checks** no canto superior direito da GUI.
3. Selecione Add Readiness Probe
4. Selecione Add Liveness Probe
5. Selecione Save

O readiness também pode ser verificado de 3 possíveis formas:

* Executando um handshake de portas
* Executando alguns dos verbos HTTP \(GET, POST, PUT, DELETE, etc\) em um contexto da aplicação
* Executando um comando ou script dentro do container

No nosso caso, vamos configurar o readiness para verificar se o contexto raiz da aplicação está respondendo conforme esperado.

Podemos fazer isso pela linha de comando também:

```
oc set probe dc/workshop-openshift --readiness --get-url=http://:8080/
```

Dessa forma, o Openshift irá tentar acessar a url raiz da aplicação e caso ela não esteja acessível, o balanceamento de carga não irá adicoinar esse container em sua lista de aplicações balanceadas.

O Openshift informa para nós por meio da console web que a aplicação não está pronta para receber requisição por meio da cor azul clara. Se o circulo ficar azul claro, quer dizer que o seu POD não passou no teste de readiness.

![](/assets/readiness.gif)

Perceba que a container ficar azul claro rapidamente e logo em seguida volta a ficar azul escurot. Isso quer dizer que por um breve período de tempo, ele não passou no readiness probe.

##### Mais informações

[https://docs.openshift.com/container-platform/3.6/dev\_guide/application\_health.html](https://docs.openshift.com/container-platform/3.6/dev_guide/application_health.html)

