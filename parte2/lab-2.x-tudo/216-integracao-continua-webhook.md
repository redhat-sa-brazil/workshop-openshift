### Integração Continua

Para que sempre que ocorra um commit o Openshift faça de forma automática o processo de build e deploy, iremos configurar  
um webhook, dessa forma o servidor git avisará o Openshift sempre que um commit novo ocorrer.

#### Configuração webhook

![](https://storage.googleapis.com/workshop-openshift/webhook.gif)

No _Openshift_:

* Selecione `Builds` &gt; `Build`
* Selecione `workshop-php`
* Selecione a aba `Configuration` e clique em copy no campo `Github Webhook URL`

![](/assets/Selection_087.png)

No _Github.com_:

* Selecione `Settings` no menu horizontal
* Selecione o `Webhooks` no menu lateral esquerdo 
* Selecione `Add Webhooks`, cole a URL copiada no campo `Payload URL`, no campo `Content Type` selecione a opção `application/json`
* Clique em `Disable SSL verification`
* Finalize no botão `Add webhook`

![](/assets/Selection_088.png)

#### Altere a aplicação

Para fazermos uma alteração na aplicação, vamos alterar a versão na página inicial da aplicação.

No `index.php` altere a linha com a versão da aplicação para versão 2.0.

```
echo "<h1>Openshift Workshop v2.0</h1>";
```

```bash
git add index.php
git commit -m "webhook adicionado"
git push
```

#### Acompanhe o rolling deployment

Observe que não ocorre indisponibilidade durante o deployment

