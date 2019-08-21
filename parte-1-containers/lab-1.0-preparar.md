# Lab 1.0 - Preparar

## Lab 1.0 - Objetivos

Preparar o ambiente local para os próximos exercícios.

## Opções de execução

Você tem uma opção disponível para a execução dos laboratórios.

### 1.1 Instalação dos pacotes necessários para o Test Drive

Acesse a sua instância conforme explicado pelo seu instrutor e, logo após, com usuário `root` execute:

```text
yum install vim wget git bash-completion docker ansible -y
```

> INFO: Caso você não esteja como root, basta executar o comando abaixo. Qualquer problema chame o instrutor.
>
> ```text
> sudo -i
> ```

Em seguida habilite o serviço do Docker Daemon no SystemD

```text
systemctl enable docker
systemctl start docker
```

