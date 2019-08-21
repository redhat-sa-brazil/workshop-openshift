# Lab 1.1 - Executar

## Lab 1.1 - Objetivos

* Buscar informações sobre o ambiente Docker
* Obter imagens de registros externos
* Manipular imagens do registro local
* Executar containers localmente

## Tarefas

### 1.1.1 - Informações do Ambiente local

Para buscarmos informações sobre o ambiente local, usa-se:

```text
docker info
```

![](https://raw.githubusercontent.com/guaxinim/test-drive-openshift/master/gitbook/assets/docker-info.png)

### 1.1.2 - Buscando Imagens dos Registries

Toda instalação do runtime Docker acompanha configuração dos Registries mais comuns. Podemos ver isso por meio do comando `docker info`.

Por padrão, o registry `docker.io` já vem configurado como podemos ver na imagem acima.

Para buscar novas imagens nos Registries configurados, usa-se:

```text
docker search fedora

docker search ubuntu
```

Nesse caso, ele irá buscar as imagens do centos no Dockerhub \(docker.io\) que já vem pré-configurado com o Docker.

![](https://raw.githubusercontent.com/guaxinim/test-drive-openshift/master/gitbook/assets/docker-search.png)

Você também pode filtrar pelo número de estrelas \(stars\) que um repo possui.

Para isso basta passar o parametro --filter

```text
docker search centos --filter=stars=10
```

![](https://raw.githubusercontent.com/guaxinim/test-drive-openshift/master/gitbook/assets/docker-search-filter.png)

No cenário acima, só existirão resultados que tenham mais que 10 estrelas.

### 1.1.3 - Baixando Imagens dos Registries

Além de nome, imagens possuem _tags_ \(sufixo separado por ':'\) que podem identificar versões ou variações de uma imagem específica. Para baixar uma imagem para o storage local de imagens, usa-se:

```text
docker pull centos:7
```

![](https://raw.githubusercontent.com/guaxinim/test-drive-openshift/master/gitbook/assets/docker-pull.png)

O comando acima é equivalente a:

```text
docker pull docker.io/centos:7
```

> INFO: Quando não especificamos qual registry queremos usar, o docker irá utilizar o que está configurado no arquivo /etc/sysconfig/docker. Quando instalado pela primeira vez, o padrão é o docker.io.

É possível também baixar imagens de outros registries quando especificamos isso na linha de comando:

No exemplo abaixo utilizaremos o registry oficial da Red Hat.

```text
docker pull registry.access.redhat.com/rhel-atomic
```

Caso você encontre o erro abaixo:

![](https://raw.githubusercontent.com/guaxinim/test-drive-openshift/master/gitbook/assets/docker-pull-rhel.png)

Ele acontece porque o link simbólico aponta para um arquivo inexistente. Para resolver isso, execute o comando abaixo:

```text
rm -f /etc/docker/certs.d/registry.access.redhat.com/redhat-ca.crt
```

Agora faça novamente o pull da imagem `rhel-atomic`:

```text
docker pull registry.access.redhat.com/rhel-atomic
```

![](https://raw.githubusercontent.com/guaxinim/test-drive-openshift/master/gitbook/assets/docker-pull-atomic.png)

No exemplo acima, ele buscará a imagem no registry `registry.access.redhat.com`

### 1.1.4 - Listando Imagens Locais

Para verificar quais imagens estão disponíveis localmente, usa-se:

```text
docker images
```

![](https://raw.githubusercontent.com/guaxinim/test-drive-openshift/master/gitbook/assets/docker-images.png)

### 1.1.5 - Removendo Imagens Locais

Para remover as imagens, ou tags, do repositório local, usa-se:

```text
docker rmi <ID/tag>
```

Vamos remover a imagem do rhel atomic baixada no lab anterior:

```text
docker images | grep rhel-atomic
```

![](https://raw.githubusercontent.com/guaxinim/test-drive-openshift/master/gitbook/assets/docker-images-grep.png)

Agora que temos o ID da imagem, podemos apagá-la:

![](https://raw.githubusercontent.com/guaxinim/test-drive-openshift/master/gitbook/assets/docker-rmi.png)

Caso a imagem já esteja sendo utilizada por um container. o Docker não irá executar essa ação e retornará um erro informando qual o id do container que está utilizando a imagem que desejamos apagar.

![](https://raw.githubusercontent.com/guaxinim/test-drive-openshift/master/gitbook/assets/docker-rm-erro.png)

Para resolver, basta remover o container que está causando problemas para a gente.

```text
docker rm <id do container>
```

![](https://raw.githubusercontent.com/guaxinim/test-drive-openshift/master/gitbook/assets/docker-rm.png)

### 1.1.6 - Executando Containers

A execução de um container significa processar os metadados da imagem e criar um ou mais processos a partir dos dados armazenados. Para tal, usa-se:

```text
docker run -it centos:7 /bin/bash
```

![](https://raw.githubusercontent.com/guaxinim/test-drive-openshift/master/gitbook/assets/docker-run-1.png)

No exemplo anterior você deve ter percebido que além de iniciar o container você entrou no isolamento. Para sair usa-se a sequência _CTRL+P+Q_. Para iniciar o container de forma _detached_, usa-se:

```text
docker run -itd centos:7 /bin/bash
```

Caso queira entrar em um container já em execução, para fazer _attach_ no processo já em execução, usa-se:

```text
docker attach <nome/ID>
```

![](https://raw.githubusercontent.com/guaxinim/test-drive-openshift/master/gitbook/assets/docker-run-2.png)

### 1.1.7 - Executando imagem do Wordpress

Uma das vantagens do uso de containers é a possibilidade de abstração da complexidade de implantação de um determinado serviço. Vamos rodar agora uma imagem do wordpress e ver o trabalho necessário para colocar esse CMS no ar.

```text
docker run --rm -p 8080:80 wordpress
```

O parametro -p exporta a porta interna do container \(80\) para a nossa máquina na porta 8080. Esse parâmetro será explicado melhor nos próximos exercícios.

![](https://raw.githubusercontent.com/guaxinim/test-drive-openshift/master/gitbook/assets/wordpress.gif)

Agora podemos abrir nosso browser na página:

[http://localhost:8080](http://<ip%20da%20sua%20VM>:8080)

> Se estiver usando uma VM na nuvem, use seu ip público para acessar o serviço.

![](https://raw.githubusercontent.com/guaxinim/test-drive-openshift/master/gitbook/assets/wordpress-localhost.png)

