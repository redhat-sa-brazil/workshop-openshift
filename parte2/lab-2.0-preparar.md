# Lab 2.0 - Objetivos

* Preparar o ambiente local para os próximos exercícios

# Tarefas

### 2.0.1 - Ambiente OpenShift

Para conseguirmos executar os próximos exercícios precisamos de um ambiente com o OpenShift instalado e disponível. Atualmente temos algumas opções disponíveis:

* [**OpenShift Origin Minishift**](https://www.openshift.org/minishift/): _Solução que permite rodar um ambiente local de OpenShift \(upstream\) em containers._
* [**Red Hat Container Development Kit \(CDK\)**](https://developers.redhat.com/products/cdk/overview/): _Equivalente ao anterior mas para a versão suportada do OpenShift._
* [**Red Hat OpenShift Online**](https://www.openshift.com/): _Oferta de cloud PaaS pública da Red Hat, com "free tier"._

Consulte o instrutor sobre qual opção usar!

### 2.0.2 - Instalar cliente do OpenShift e Git

Além do acesso ao ambiente, precisamos também** instalar alguns componentes adicionais na nossa máquina virtual** criada na parte 1 desse material. Basicamente vamos instalar o cliente CLI do OpenShift e do Git:

```
# yum install centos-release-openshift-origin
# yum install origin-clients git
```

Caso você queira instalar o cliente do OpenShift na sua máquina real, ao invés de virtual, você pode obter os pacote em:

* [**https://www.openshift.org/download.html**](https://www.openshift.org/download.html)



