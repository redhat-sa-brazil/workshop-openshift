# Parte 3 - OpenShift \(Ops\)

Openshift é, essencialmente, uma solução para a área de infra-estrutura. Trabalhar com Containers é fantástico para o negócio, para os desenvolvedores mas para a área de operações e infra-estrutura, se não gerenciado adequadamente, pode tornar-se um pesadelo. Implementar um container é tarefa fácil. Operacionalizar containers não.

Todo o trabalho da Red Hat para Openshift gira em torno de manter o gerenciamento dos containers com foco em:

* Segurança
* Estabilidade
* Escalabilidade
* Robustez

O objetivo deste workshop é, de uma forma rápida, apresentar os principais conceitos da solução, orientado para a área de infra-estrutura, e trabalhar com a operação básica do openshift, incluindo instalação, configuração e operação da plataforma.

## Conceitos Basicos

**O que é e por que preciso de Kubernetes?**

Com o crescimento no uso de containers, o gerenciamento manual pode tornar-se confuso e por vezes inviável. Se gerenciar 100 máquinas virtuais é complicado, 1000 containers será uma tarefa impossível manter a segurança, estabilidade, escalabilidade e robustez do ambiente. Kubernetes é um orquestrador de containers que permite, entre outras funções, orquestração e escalonamento de containers , gerenciamento de storage persistente, descoberta e catálogo de serviços sobre um cluster de nós físicos ou virtuais. 

Originalmente desenvolvido pelo Google, foi "doado" para a CNCF \(Cloud Native Computing Foundation\) permitindo que seu codigo aberto receba contribuições da comunidade. \(Kubernetes foi considerado um dos projetos open-source mais rapidamente desenvolvidos da historia\).

Além disso, Kubernetes é hoje a plataforma de orquestração mais avançada e com maior número de contribuições da comunidade, sendo a Red Hat um dos maiores contribuidores.

**Por que preciso de Openshift além de Kubernetes?**

Openshift permite o uso corporativo de Kubernetes, introduzindo segurança, colaboração, networking \(nativo\), gerenciamento de registry, monitoração, CI/CD e uma série de outras facilidades. Em resumo, Openshift permite utilizar Kubernetes em produção adicionando todas as funções que mais importam para a gestão corporativa dos containers.

![](/assets/openshif_features.png)

**Arquitetura Openshift**



![](/assets/parte_3_arquitetura_ocp.png)

Componentes Principais:

**Kubernetes** - gerenciador principal do cluster Openshift, Kubernetes fornece a infra-estrutura de nós Master e Nodes que sustentam a orquestração dos containers

**Master** - Nó do Kubernetes responsável por controlar o cluster, incluindo API server, controler manager server e etcd.

**Node** - Nó responsável por hospedar os containers. Podem receber "labels" que usualmente são utilizados para determinar funções dos nós e consequentemente concentrar funções mais específicas. Ex: Storage Nodes, Infra Nodes, App Nodes e etc.

**Container Registry **- Base de imagens de containers. OCP suporta Docker Hub, Private Registries e fornece OCR \(Openshift Container Registry\)

**Console Web **- Web UI client da API Openshift.

Terminologia Openshift

* Aplicação - Basicamente é a aplicação Web que irá rodar no Openshift. Openshift é focado em aplicações Web, sendo assim, as portas associadas as aplicações estão basicamente limitadas a 80, 443 e eventualmente, 22. Consiste, internamente, em tudo o que voce precisa para fazer sua aplicação funcionar. Deployments, Pods, Services, Routes e etc, assim como as ligações entre elas.
* Pods e Cluster



