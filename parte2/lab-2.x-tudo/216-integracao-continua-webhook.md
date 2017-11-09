### Integração Continua

Para que sempre que ocorra um commit o Openshift faça de forma automátia o processo de build e deploy, iremos configurar  
um webhook, dessa forma o servidor git avisará o Openshift sempre que um commit novo ocorrer.

#### Configuração webhook

![](https://storage.googleapis.com/workshop-openshift/webhook.gif)

No _Openshift_:

* Selecione `Builds` &gt; `Build`
* Selecione `workshop-php`
* Selecione a aba `Configuration` e clique em copy no campo `Github Webhook URL`

No _Github.com_:

* Selecione `Settings` no menu horizontal
* Selecione o `Webhooks` no menu lateral esquerdo 
* Selecione `Add Webhooks`, cole a URL copiada no campo `Payload URL`, no campo `Content Type` selecione a opção `application/json`
* Finalize no botão `Add webhook`

#### Altere a aplicação

Para fazermos uma alteração na aplicação, vamos inserir a versão na página inicial da aplicação.

No `index.php` insira uma linha com a versão da aplicação.

```
echo "<h4>Versão 2.0</h4> ";
```

#### Acompanhe o rolling deployment

Observe que não ocorre indisponibilidade durante o deployment

