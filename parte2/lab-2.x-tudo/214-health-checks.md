### Health Checks

Componentes de software ficam indisponíveis por varias razões, como por exemplo falha de comunicação, erro de configuração ou problemas com dependências externas como banco de dados ou broker de mensagens, o Openshift possui dois recursos bastante poderosos para fazer o health checks de aplicações. O primeiro é que iremos abordar é o Liveness e em seguida o Readiness.

#### Liveness

O liveness verifica se o container ainda está em execução \(de forma sadia\). Se a verificação falhar este container é morto e sujeitado a política de restart que por padrão é "always". Logo o comportamento padrão é se acontecer alguma falha o container é reiniciado.

#### Readiness

O readiness define quando que o container está pronto para receber requisições. Caso a verificação do readiness falhe nenhuma requisição será direcionado para este container até que a verificação seja satisfeita.

#### Configuração no Openshift

![](https://storage.googleapis.com/workshop-openshift/ocp-health-checks.gif)

1. Selecione no menu vertical esquerdo a opção **Deployments &gt; openshift-workshop**
2. Selecione **Actions &gt; Edit Health Checks** no canto superior direito da GUI.
3. Selecione Add Readiness Probe
4. Selecione Add Liveness Probe
5. Selecione Save

##### Mais informações

[https://docs.openshift.com/container-platform/3.6/dev\_guide/application\_health.html](https://docs.openshift.com/container-platform/3.6/dev_guide/application_health.html)

