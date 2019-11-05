
# Introdução

## Afinal, o que são containers

A tecnologia de container Linux é, na verdade, um conjunto de capacidades
que permitem o isolamento e contenção de aplicações. Apesar da recente
exposição do termo, essa é uma tecnologia que vem sendo aprimorada desde
o UNIX, com o chroot, ou do BSD, com o Jails.

![Virtualizacao](../images/virtu.png)  ![Containers](../images/containers.png)

Ao contrário da tecnologia de virtualização que encapsula um
sistema operacional completo em cima de um hardware virtual
para usar como casulo para aplicações, containers usam de
funcionalidades nativas do kernel Linux
para garantir isolamento e contenção das aplicações,
como por exemplo:

- Namespaces:

Permite criar uma abstração de um recurso de sistema
global particular e fazê-lo aparecer como uma instância separada
para processos dentro de um namespace. Conseqüentemente,
vários containers podem usar o mesmo recurso simultaneamente
sem criar um conflito.

- Control Groups (cgroups):

Permite agrupar processos para fins
de gerenciamento de recursos do sistema. Os Cgroups alocam o
tempo da CPU, a memória do sistema, a largura de banda da rede
ou combinações destes entre os grupos de tarefas definidos
pelo usuário.

- SELinux:

Fornece uma separação segura, pois impede que os
processos raiz dentro do container interfiram com outros processos globais.

- Linux Capabilities:

Permite a limitação dos privilégios
disponíveis a processos que rodam como root em pequenos grupos de privilégios.
Desse modo, um processo rodando com privilégios de root pode ser limitado
a obter apenas as permissões mínimas que ele precisa para executar suas tarefas.

Apesar de ser uma tecnologia antiga, os containers ganharam mais popularidade
hoje em dia principalmente pela sua portabilidade. Soluções como Docker
ficaram realmente atrativas quando permitiram que um container pudesse
ser compartilhado entre infraestruturas heterogêneas. Isso foi possível
graças a criação do
conceito de imagem, que será nosso próximo tópico nesse guia.

Apesar das diversas funcionalidades, existem situações que podem
não funcionar conforme esperado quando executamos, por exemplo,
um container com Ubuntu em um servidor hospedeiro rodando CentOS.
Vale sempre lembrar que, container é linux e sua execução depende
das bibliotecas e principalmente do kernel do host.
Há muitos mecanismos de contêiner disponíveis para gerenciar e executar
contêineres individuais, incluindo *Rocket, Drawbridge, LXC, Docker e Podman.*

Com o surgimento de novas tecnologias de containers e com uma grande
demanda por parte do mercado por esse tipo de ferramenta, foi criado
uma especificação que  direciona como os containers e imagens
devem ser executados/criados. A OCI (Open Container Iniciative) foi
criada em 2015 e se propõe a criar uma padrão de mercado para
runtime e images.

__Veja abaixo algumas vantagens importantes para o uso de contêineres:__

- Baixa área de ocupação do hardware:

Os contêineres usam recursos internos do SO para criar um ambiente isolado
em que os recursos são gerenciados usando recursos do SO. Essa abordagem
minimiza a quantidade de sobrecarga de CPU e na memória em comparação a
um hipervisor de máquina virtual. A execução de um aplicativo em uma VM
é uma maneira de criar isolamento a partir do ambiente de execução, mas
isso requer uma camada pesada de serviços para suportar o mesmo isolamento
de baixa área de ocupação de hardware que é oferecido por contêineres.

- Isolamento de ambiente:

Os contêineres funcionam em um ambiente fechado onde as alterações feitas
no SO de host ou outros aplicativos não afetam o contêiner. Como as bibliotecas
necessárias para um contêiner são autocontidas, o aplicativo pode ser executado
sem interrupções. Por exemplo, cada aplicativo pode existir em seu próprio
contêiner com seu próprio conjunto de bibliotecas. Uma atualização feita
em um contêiner não afeta outros contêineres.

- Implantação rápida:

Os contêineres são implantados rapidamente porque não há necessidade
de instalar todo o sistema operacional subjacente. Normalmente, para
dar suporte ao isolamento, uma nova instalação do SO é necessária em um
host físico ou VM, e qualquer atualização simples pode precisar de uma
reinicialização total do SO. A reinicialização de um contêiner não
exige a interrupção de nenhum serviço no SO de host.

- Implantação em múltiplos ambientes:

Em um cenário tradicional de implantação usando um único host,
qualquer diferença de ambiente pode interromper o aplicativo.
Ao usar contêineres, no entanto, todas as dependências de aplicativo
e configurações de ambiente são encapsuladas na imagem do contêiner.

- Reusabilidade:

O mesmo contêiner pode ser usado sem a necessidade de
configurar um SO completo.
Por exemplo, o mesmo contêiner de banco de dados que fornece um serviço
de banco de dados de produção pode ser usado por cada desenvolvedor
para criar um banco de dados de desenvolvimento durante o desenvolvimento
do aplicativo. Ao usar contêineres, não há mais a necessidade de manter
servidores de bancos de dados de produção e desenvolvimento separados.
Uma única imagem de contêiner é usada para criar instâncias do serviço
de banco de dados.
