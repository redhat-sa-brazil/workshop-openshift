# Lab 1.2 - Objetivos

* Buscar informações containers em execução
* Executar processos adicionais em containers ativos
* Mapear volumes locais aos containers
* Mapear rede aos containers

# Tarefas

### 1.2.1 - Monitorando Containers

Para buscar mais informações sobre os containers em execução, usa-se:

```
# docker ps
```

![](/assets/Selection_025.png)

No exemplo anterior não são listados containers terminados. Para visualizar a listagem completa, usa-se:

```
# docker ps -a
```

![](/assets/Selection_026.png)

Para visualizar os processos em execução dentro de um container, usamos:

```
# docker top <id/nome>
```

![](/assets/Selection_027.png)

Também podemos inspecionar os metadados do container, ou de uma imagem, através de:

```
# docker inspect <id/nome/tag>
```

![](/assets/gustavo@localhost: ~_028.png)

### 1.2.2 - Execução Ad-Hoc

Também podemos conectar em um container em execução e executar processos adicionais usando:

```
# docker exec -it <container-id> /bin/sh
```

![](/assets/Selection_029.png)

### 1.2.3 - Adicionando Persistência

Containers são essencialmente efêmeros. Entretanto, podemos mapear diretórios a eles e ter mecanismos de persistência de dados. Esse mecanismo é usado através do comando:

```
# docker run -it -v /tmp/:/tmp/host:z centos:7
```

No exemplo acima, o diretório /tmp/host do container será mapeado para o diretório /tmp no host hospedeiro

### 1.2.4 - Mapeando Rede

Por padrão, os containers utilizam de redes privadas locais no host hospedeiro. Dessa forma se faz necessário usar mapeamento de portas para expor serviços de rede, como uma aplicação web:

```
# docker run -it -p 8080:80 httpd
```

No exemplo acima, a porta 80 do container será exposta na porta 8080 do host hospedeiro

Ao invés de mapear manualmente, podemos usar portas aleatórias:

```
# docker run -it -P httpd
```



