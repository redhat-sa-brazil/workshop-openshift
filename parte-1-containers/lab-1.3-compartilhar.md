# Lab 1.3 - Compartilhar

## Lab 1.3 - Objetivos

* Criar imagens a partir de outras existentes
* Publicar imagens em registros remotos

## Tarefas

### 1.3.1 - Construir Novas Imagens

Além de consumir imagens já prontas, podemos construir nossas próprias imagens. Para isso, precisamos criar um arquivo chamado _Dockerfile_, onde especificamos todas as etapas de construção da nova imagem a partir de diretivas. As mais comuns são:

* **LABEL**: _Pode ser usado para adicionar metadados à imagem \(autor, versão, descrição\)._
* **FROM**: _Especifica qual imagem será usada como base._
* **RUN**: _Executa comandos dentro da imagem._
* **ADD/COPY**: _Adiciona arquivos/diretórios dentro da imagem._
* **EXPOSE**: _Especifica quais serviços de rede serão expostos._
* **USER**: _Determina qual o usuário será usado para execução dos comandos._
* **CMD**: _Especifica qual o comando que será executado por padrão na nova imagem._

Para essa atividades, vamos criar os seguintes diretórios:

```text
mkdir -p ~/workshop-openshift/lab1.3/src && cd ~/workshop-openshift/lab1.3/src
```

No subdiretório `~/workshop-openshift/lab1.3/src`, vamos adicionar dois arquivos, `app.py` e `requirements.txt`, com os seguintes conteúdos \(respectivamente\):

```python
#! /usr/bin/env python

from flask import Flask

app = Flask(__name__)

@app.route('/')
def hello_world():
    return "Hello, world!"

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=8080)
```

e

```text
click==6.7
Flask==0.12.2
itsdangerous==0.24
Jinja2==2.9.6
MarkupSafe==1.0
```

Para agilizar a criação dos arquivos, basta executar os comandos abaixo:

```python
cat <<EOF > ~/workshop-openshift/lab1.3/src/app.py
#! /usr/bin/env python

from flask import Flask

app = Flask(__name__)

@app.route('/')
def hello_world():
    return "Hello, world!"

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=8080)
EOF
```

e

```python
cat <<EOF > ~/workshop-openshift/lab1.3/src/requirements.txt
click==6.7
Flask==0.12.2
itsdangerous==0.24
Jinja2==2.9.6
MarkupSafe==1.0
Werkzeug==0.12.2
EOF
```

Na raiz do diretório `~/workshop-openshift/lab1.3/`, vamos adicionar um arquivo de texto com nome `Dockerfile` com o seguinte conteúdo:

```text
FROM fedora:27

LABEL maintainer="do-not-reply@redhat.com"
LABEL version="1.0"

RUN mkdir /var/www

ADD src/. /var/www

RUN pip3 install -r /var/www/requirements.txt

EXPOSE 8080

USER 12345

CMD ["python3", "/var/www/app.py"]
```

Para agilizar a criação do arquivos, podemos utilizar:

```text
cat <<EOF > ~/workshop-openshift/lab1.3/Dockerfile
FROM fedora:27

LABEL maintainer="do-not-reply@redhat.com"
LABEL version="1.0"

RUN mkdir /var/www

ADD src/. /var/www

RUN pip3 install -r /var/www/requirements.txt

EXPOSE 8080

USER 12345

CMD ["python3", "/var/www/app.py"]
EOF
```

Para iniciarmos o processo de construção da nova imagem, usa-se:

```text
cd ~/workshop-openshift/lab1.3
docker build -t workshop-openshift .
```

![](https://raw.githubusercontent.com/guaxinim/test-drive-openshift/master/gitbook/assets/docker-build.png)

Valide se sua imagem está funcionando corretamente por meio do comando:

```text
docker run --rm workshop-openshift
```

A saída desse comando é algo como:

![](https://raw.githubusercontent.com/guaxinim/test-drive-openshift/master/gitbook/assets/docker-run-rm.png)

Verifique a sua imagem nova no registro local:

```text
docker images | grep workshop-openshift
```

![](https://raw.githubusercontent.com/guaxinim/test-drive-openshift/master/gitbook/assets/docker-images-grep-2.png)

Podemos ver que é a nossa imagem que foi construida recentemente conforme destacado na foto acima.

### 1.3.2 - Publicar Imagens no Registry

Para publicar uma imagem em um registro remoto, muitas das vezes é necessário autenticação. Para tal, usamos:

> _note_: caso não possua uma conta no Docker Hub, acesse [https://hub.docker.com/register](https://hub.docker.com/register) e crie um conta pessoal.

```text
docker login docker.io
```

Depois de autenticados, precisamos colocar um tag na nossa imagem usando a convenção `registry/username/image:tag`:

```text
docker tag workshop-openshift docker.io/<username>/workshop-openshift
```

E depois já podemos enviar nossa imagem:

```text
docker push docker.io/<username>/workshop-openshift
```

