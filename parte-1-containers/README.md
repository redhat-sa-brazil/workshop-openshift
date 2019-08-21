# Parte 1 - Linux Containers

## Afinal, o que são containers?

A tecnologia de container Linux é, na verdade, um conjunto de capacidades que permitem o isolamento e contenção de aplicações. Apesar da recente exposição do termo, **essa é uma tecnologia que vem sendo aprimorada desde o UNIX, com o chroot, ou do BSD, com o Jails**.

![](https://raw.githubusercontent.com/guaxinim/test-drive-openshift/master/gitbook/assets/virtualization-vs-containers.png)

Ao contrário da tecnologia de virtualização que encapsula um sistema operacional completo em cima de um hardware virtual para usar como casulo para aplicações, **containers usam de funcionalidades nativas do kernel Linux para garantir isolamento e contenção das aplicações**:

* **Namespaces:** _Permite criar uma abstração de um recurso de sistema global particular e fazê-lo aparecer como uma instância separada para processos dentro de um namespace. Conseqüentemente, vários containers podem usar o mesmo recurso simultaneamente sem criar um conflito._
* **Control Groups \(cgroups\):** _Permite agrupar processos para fins de gerenciamento de recursos do sistema. Os Cgroups alocam o tempo da CPU, a memória do sistema, a largura de banda da rede ou combinações destes entre os grupos de tarefas definidos pelo usuário._
* **SELinux:** _Fornece uma separação segura, pois impede que os processos raiz dentro do container interfiram com outros processos globais._
* **Linux Capabilities:** Permite a limitação dos privilégios disponíveis a processos que rodam como root em pequenos grupos de privilégios. Desse modo, um processo rodando com privilégios de root pode ser limitado a obter apenas as permissões mínimas que ele precisa para executar suas tarefas.

Entendendo essas funcionalidades, podemos perceber que **containers são linux** já que estão intimamente acoplados as features nativas do kernel do linux.

Apesar de ser uma tecnologia antiga, os containers ganharam mais popularidade hoje em dia principalmente pela sua **portabilidade**. Soluções como [Docker](https://www.docker.com/) ficaram realmente atrativas quando permitiram que um container pudesse ser compartilhado entre infraestruturas heterogêneas. Isso foi possível graças a criação do conceito de imagem, que será nosso próximo tópico nesse guia.

Apesar da grande quantidade de informações que dizem ser possível a portabilidade de containers entre diferentes sistemas operacionais, ela não é sempre obtida na prática. Existem situações que podem não funcionar conforme esperado quando executamos, por exemplo, um container com Ubuntu em um servidor hospedeiro rodando CentOS. Além disso, precisamos garantir que a [mesma versão do Docker esteja rodando nos servidores](https://www.infoworld.com/article/3223073/containers/what-does-container-portability-really-mean.html) e até mesmo o tempo de vida da imagem pode influenciar nesse equação. Vale sempre lembrar que, [container é linux](https://www.redhat.com/en/blog/containers-are-linux) e sua execução depende das bibliotecas e principalmente do kernel do host.

Além do Docker, existem também outras soluções de containers no mercado:

* [RKT](https://coreos.com/rkt/) - CoreOS
* [LXD](https://www.ubuntu.com/containers/lxd) - Canonical
* [CRI-O](https://cri-o.io/) - Red Hat

Com o surgimento de novas tecnologias de containers e com uma grande demanda por parte do mercado por esse tipo de ferramenta, foi criado uma especificação que norteia e direciona como os containers e imagens devem ser executados/criados. A [OCI](https://www.opencontainers.org/) \(Open Container Iniciative\) foi criada em 2015 e se propõe a criar uma padrão de mercado para runtime e images. Grandes empresas como Google, Red Hat, Intel e Amazon apoiam essa iniciativa.

Com o foco em evitar o lock-in, é altamente recomendável que qualquer empresa hoje utilize qualquer runtime que esteja compliance com a especificação OCI. Dessa forma, em qualquer momento pode ser trocada a runtime de container sem impactar o ambiente operacional, garantindo assim a liberdade de escolha do usuário.

## O que são imagens e como funcionam?

Os **containers são entidades efêmeras por natureza**, baseadas em imagens imutáveis. Estas armazenam informações de **metadados \(informações e parâmetros\)** e os **dados \(executáveis, bibliotecas e arquivos\)** que serão usados com o container.

![](https://raw.githubusercontent.com/guaxinim/test-drive-openshift/master/gitbook/assets/docker-layered-filesystem.png)

Como mecanismo de otimização, de espaço e de performance, essas imagens são construídas em **camadas sobrepostas, também imutáveis**. Dessa forma conseguimos aproveitar camadas comuns entre as diferentes imagens, **poupando espaço de armazenamento e melhorando a performance**.

Apesar da possibilidade de escrita de dados na última camada conforme mostrado no desenho acima, todos os dados são perdidos após a finalização do container.

## Onde as imagens ficam armazenadas?

Existem dois tipos de repositórios, ou registros, importantes para armazenamento das imagens de containers: **registro local \(ou storage local\)** e **registros remotos \(públicos/privados\)**.

O **storage local é um espaço de armazenamento especial que reside no mesmo host que executa os containers**. Esse é usado para armazenas as imagens que serão usadas para executar containers nessa máquina, servindo como uma camada de cache. Esse é o primeiro repositório a ser consultado em busca de imagens.

Os **registros remotos são servidores, públicos ou privados, responsáveis por compartilhar imagens construidas por entidades e/ou usuários**. Estes registros podem permitir não só o acesso para download de imagens, mas também envio de imagens novas por usuários autenticados/autorizados. Dentre os mais famosos temos:

* [**https://registry.access.redhat.com**](https://registry.access.redhat.com)
* [**https://hub.docker.com**](https://hub.docker.com)
* [**https://registry.fedoraproject.org**](https://registry.fedoraproject.org)

Geralmente os registros remotos são executados na **porta 5000.**

