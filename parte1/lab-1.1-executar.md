# Lab 1.1 - Objetivos

* Buscar informações sobre o ambiente Docker
* Obter imagens de registros externos
* Manipular imagens do registro local
* Executar containers localmente

# Tarefas

### 1.1.1 - Informações do Ambiente local

Para buscarmos informações sobre o ambiente local, usa-se:

```
# docker info
```

![](/assets/gustavo@localhost: ~_016.png)

### 1.1.2 - Buscando Imagens dos Registries

Toda instalação do runtime Docker acompanha configuração dos Registries mais comuns. Para buscar novas imagens nos Registries configurados, usa-se:

```
# docker search centos
```

![](/assets/gustavo@localhost: ~_017.png)

### 1.1.3 - Baixando Imagens dos Registries

Além de nomes, imagens possuem _tags_ \(sufixo separado por ':'\) que podem identificar versões ou variações de uma imagem específica. Para baixar uma imagem para o repositório local de imagens, usa-se:

```
# docker pull centos:7
```

![](/assets/gustavo@localhost: ~_018.png)

### 1.1.4 - Listando Imagens Locais

Para verificar quais imagens estão disponíveis localmente, usa-se:

```
# docker images
```

![](/assets/gustavo@localhost: ~_019.png)

### 1.1.5 - Removendo Imagens Locais

Para remover as imagens, ou tags, do repositório local, usa-se:

```
# docker rmi <ID/tag>
```

![](/assets/gustavo@localhost: ~_021.png)

### 1.1.6 - Executando Containers

A execução de um container significa processar os metadados da imagem e criar um ou mais processos a partir dos dados armazenados. Para tal, usa-se:

```
# docker run -it centos:7 /bin/bash
```

![](/assets/@ea0db5938e36:-_022.png)

No exemplo anterior você deve ter percebido que além de iniciar o container você entrou no isolamento. Para sair usa-se a sequência _CTRL+P+Q_. Para iniciar o container de forma _detached_, usa-se:

```
# docker run -itd centos:7 /bin/bash
```

Caso queira entrar em um container já em execução, para fazer _attach_ no processo já em execução, usa-se:

```
# docker attach <nome/ID>
```

![](/assets/docker attach c548bf3b3d4b9b5d68c8f3abfcb78e602bbce246e88c3d6fdfbbc3cc4c692b0_023.png)

