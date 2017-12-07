### Image Stream

O Openshift permite monitorar e realizar algumas ações assim que uma imagem é atualizada no seu registry interno. Se uma aplicação tiver uma falha de segurança crítica, e existirem 200 containers desse sistema, basta que a sua respectiva imagem seja atualizada no registry que todos os 200 containers serão atualizados automaticamente.

Todo esse poder de notificação, só existe graças a um componente chamado Image Stream. Um Image Stream é um repositório virtual que contém as informações das suas imagens.

Nessa demo iremos criar uma imagem base baseado no Httpd e, baseado nela, iremos criar duas aplicações. Logo em seguida simularemos uma atualização da imagem base, o que acarretará na construção \(build\) e atualização das duas aplicações que dependem dela.

#### Preparando o ambiente

Para que essa demo funcione conforme esperado, é necessário liberar a permissão de rodar os containers como root.

```
oc adm policy add-scc-to-user anyuid -z default -n myproject
```

Vamos importar o template que iniciará o build das 3 imagens necessárias.

```
oc create -f https://raw.githubusercontent.com/luszczynski/openshift-image-stream-example/master/template.yaml
```

Agora já podemos executar o template

```
oc new-app --template=base-image-example --param=GIT_URL=https://github.com/luszczynski/openshift-image-stream-example.git -n myproject
```

#### Atualizando a base image \(TODO\)



