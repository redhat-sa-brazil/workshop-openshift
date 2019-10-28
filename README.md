# Introdução

## O que é isso?

Esse material é usado para capacitação e transferência de conhecimento de clientes e parceiros da Red Hat Brasil em **OpenShift**, aplicável tanto ao [**Red Hat OpenShift Container Platform**](https://www.openshift.com/container-platform/index.html) \(enterprise\) quanto ao [**OpenShift Origin**](https://www.openshift.org/) \(community\).

## O que são v3.x e v4.x?

Esse repositório inclui material para workshops em diferentes versões do Red Hat OpenShift, que foram construidas de forma completamente distintas. Essas versões são mantidas em `branches` diferentes neste repositório. Em resumo, temos:

- **v3.11**: *Versão atual, disponível em https://redhatbsb.gitbook.io/workshop-openshift/.*
- **v3.6 (obsoleta)**: *Versão sem manutenção, disponível em https://redhat-sa-brazil.gitbook.io/workshop-openshift/.*

A branch **develop** contém o conteúdo em desenvolvimento. A branch **master** deveria refletir a última versão estável, que atualmente é a **v3.11**, mas estamos com preguiça para rebase com conflitos (será resolvido no lançamento do **v4.2**).

## Por que dessa forma?

Inspirados na cultura open-source, acreditamos que, ao disponibilizar o material de forma aberta, podemos **evoluir o workshop de forma colaborativa e alinhado com as necessidades dos nossos clientes, parceiros e a comunidade**.

Este trabalho está licenciado sob a [**Licença Atribuição-NãoComercial-CompartilhaIgual 4.0 Internacional Creative Commons \(CC BY-NC-SA 4.0\)**](https://creativecommons.org/licenses/by-nc-sa/4.0/deed.pt_BR).

## Como usar?

**Não existe uma maneira certa ou errada de usar o conteúdo deste material.** Você poderia seguir como um roteiro independente, usando a sua máquina particular como ambiente de experimentação, ou você pode se reunir com colegas e compartilhar a experiência em um dos eventos de Test-Drive Workshops.

Para conseguir aproveitar o material, você precisará:

* _Reserve entre **4-6 horas** para discussão dos assuntos e execução das atividades._
* _Tenha um computador com **acesso à Internet** (http/https) e **editor de arquivos YAML** (Vim, VSCode, Notepad++)._
* _Caso não tenha acesso a um ambiente **Red Hat OpenShift 4**, você pode usar o [**Red Hat CodeReady Containers**](https://github.com/code-ready/crc)._

Todo o roteiro pode ser acessado através do [**Github Pages**](https://redhat-sa-brazil.github.io/workshop-openshift), ou utilizando o [**docsify.js**](https://docsify.js.org) a partir da cópia deste repositório.

```bash
$ git clone https://github.com/redhat-sa-brazil/workshop-openshift.git
$ cd workshop-openshift
$ docsify serve docs
```

## Posso contribuir?

**Sem dúvida!** Você pode fazer uso da funcionalidade de "Issues" direto do repositório fonte no [**Github**](https://github.com/redhat-sa-brazil/workshop-openshift), mas por favor siga o fluxo de trabalho do [**GitFlow**](https://datasift.github.io/gitflow/IntroducingGitFlow.html). 
