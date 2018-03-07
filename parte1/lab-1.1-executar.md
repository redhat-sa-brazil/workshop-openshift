# Lab 1.1 - Objetivos

* Buscar informações sobre o ambiente Docker
* Obter imagens de registros externos
* Manipular imagens do registro local
* Executar containers localmente

# Tarefas

### 1.1.1 - Informações do Ambiente local

Para buscarmos informações sobre o ambiente local, usa-se:

```
docker info
```

![](/assets/gustavo@localhost: ~_016.png)

### 1.1.2 - Buscando Imagens dos Registries

Toda instalação do runtime Docker acompanha configuração dos Registries mais comuns. Para buscar novas imagens nos Registries configurados, usa-se:

```
docker search centos
```

Nesse caso, ele irá buscar as imagens do centos no Dockerhub que já vem pré-configurado com o Docker.![](/assets/gustavo@localhost: ~_017.png)Você também pode filtrar pelo número de estrelas \(stars\) que um repo possui.

Para isso basta passar o parametro --filter

```
docker search centos --filter=stars=10
```

![](/assets/Selection_081.png)

Só existirão resultados que tenham mais que 10 estrelas.

### 1.1.3 - Baixando Imagens dos Registries

Além de nome, imagens possuem _tags_ \(sufixo separado por ':'\) que podem identificar versões ou variações de uma imagem específica. Para baixar uma imagem para o storage local de imagens, usa-se:

```
docker pull centos:7
```

![](/assets/Selection_216.png)

É possível também baixar imagens de outros registries quando especificamos isso na linha de comando:

No exemplo abaixo utilizaremos o registry oficial da Red Hat.

```
docker pull registry.access.redhat.com/rhel-atomic
```

Caso você encontre o erro abaixo:

![](/assets/Selection_214.png)

Ele acontece porque o registry da Red Hat exige certificado SSL. Para resolver isso, instale o seguinte pacote:

```
yum install python-rhsm-certificates -y
```

Agora faça novamente o pull da imagem `rhel-atomic`:

```
docker pull registry.access.redhat.com/rhel-atomic
```

![](/assets/Selection_082.png)No exemplo acima, ele buscará a imagem no registry `registry.access.redhat.com`

### 1.1.4 - Listando Imagens Locais

Para verificar quais imagens estão disponíveis localmente, usa-se:

```
docker images
```

![](/assets/Selection_215.png)

### 1.1.5 - Removendo Imagens Locais

Para remover as imagens, ou tags, do repositório local, usa-se:

```
docker rmi <ID/tag>
```

Vamos remover a imagem do rhel atomic baixada no lab anterior:

```
docker images | grep rhel-atomic
```

![](/assets/Selection_303.png)Agora que temos o ID da imagem, podemos apagá-la:

![](/assets/Selection_304.png)

Caso a imagem já esteja sendo utilizada por um container. o Docker não irá executar essa ação e retornará um erro informando qual o id do container que está utilizando a imagem que desejamos apagar.

![](/assets/Selection_083.png)Para resolver, basta remover o container que está causando problemas para a gente.

```
docker rm <id do container>
```

![](/assets/Selection_085.png)

### 1.1.6 - Executando Containers

A execução de um container significa processar os metadados da imagem e criar um ou mais processos a partir dos dados armazenados. Para tal, usa-se:

```
docker run -it centos:7 /bin/bash
```

![](/assets/Selection_217.png)

No exemplo anterior você deve ter percebido que além de iniciar o container você entrou no isolamento. Para sair usa-se a sequência _CTRL+P+Q_. Para iniciar o container de forma _detached_, usa-se:

```
# docker run -itd centos:7 /bin/bash
```

Caso queira entrar em um container já em execução, para fazer _attach_ no processo já em execução, usa-se:

```
# docker attach <nome/ID>
```

![](/assets/Selection_218.png)

### 1.1.7 - Executando imagem do Wordpress

Uma das vantagens do uso de containers é a possibilidade de abstração da complexidade de implantação de um determinado serviço. Vamos rodar agora uma imagem do wordpress e ver o trabalho necessário para colocar esse CMS no ar.

```
docker run --rm -p 8080:80 wordpress
```

O parametro -p exporta a porta interna do container \(80\) para a nossa máquina na porta 8080. Esse parâmetro será explicado melhor nos próximos exercícios.![](/assets/wordpress.gif)Agora podemos abrir nosso browser na página: [http://localhost:8080](http://localhost:8080)

> _nota_: caso esteja usando uma VM local acesse a URL utilizando o endereço IP da sua VM. Execute o comando `ip a s` dentro do shel da VM para saber o IP da rede interna do VirtualBox.
>
> Se estiver usando uma VM na nuvem, use seu ip público para acessar o serviço.

![](/assets/Selection_047.png)

