# Parte 1 - Containers

## Afinal, o que são containers?

A tecnologia de container Linux é, na verdade, um conjunto de capacidades que permitem o isolamento e contenção de aplicações. Apesar da recente exposição do termo, **essa é uma tecnologia que vem sendo aprimorada desde o UNIX, com o chroot, ou do BSD, com o Jails**.

![](/parte1/extras/virtualization-vs-containers.png)

Ao contrário da tecnologia de virtualização que encapsula um sistema operacional completo em cima de um hardware virtual para usar como casulo para aplicações, **containers usam de funcionalidades nativas do kernel Linux para garantir isolamento e contenção das aplicações**:

* **Namespaces:** _Permite criar uma abstração de um recurso de sistema global particular e fazê-lo aparecer como uma instância separada para processos dentro de um namespace. Conseqüentemente, vários containers podem usar o mesmo recurso simultaneamente sem criar um conflito._

* **Control Groups \(cgroups\):** _Permite agrupar processos para fins de gerenciamento de recursos do sistema. Os Cgroups alocam o tempo da CPU, a memória do sistema, a largura de banda da rede ou combinações destes entre os grupos de tarefas definidos pelo usuário._

* **SELinux:** _Fornece uma separação segura, pois impede que os processos raiz dentro do container interfiram com outros processos globais._

## Como as imagens funcionam?

Os **containers são entidades efêmeras por natureza**, baseadas em imagens imutáveis. Estas armazenam informações de **metadados \(informações e parâmetros\) **e os **dados \(executáveis, bibliotecas e arquivos\)** que serão usados com o container.

![](/parte1/extras/docker-layered-filesystem.png)

Como mecanismo de otimização, de espaço e de performance, essas imagens são construídas em **camadas sobrepostas, também imutáveis**. Dessa forma conseguimos aproveitar camadas comuns entre as diferentes imagens, **poupando espaço de armazenamento e melhorando a performance**.

## Onde essas imagens ficam armazenadas?

Existem dois tipos de repositórios, ou registros, importantes para armazenamento das imagens de containers: **registro local \(ou storage local\)** e **registros remotos \(públicos/privados\)**.

O **registro local é um espaço de armazenamento especial que reside no mesmo host que executa os containers**. Esse é usado para armazenas as imagens que serão usadas para executar containers nessa máquina, servindo como uma camada de cache. Esse é o primeiro repositório a ser consultado em busca de imagens.

Os **registros remotos são servidores, públicos ou privados, responsáveis por compartilhar imagens construidas por entidades e/ou usuários**. Estes registros podem permitir não só o acesso para download de imagens, mas também envio de imagens novas por usuários autenticados/autorizados. Dentre os mais famosos temos:

* [https://hub.docker.com](https://hub.docker.com)
* [https://registry.access.redhat.com](https://registry.access.redhat.com)
* [https://registry.fedoraproject.org](https://registry.fedoraproject.org)



