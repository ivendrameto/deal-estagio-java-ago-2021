# API - Definição dos recursos (API) da aplicação

[Voltar](./index.md)

## Referências
Item   | Exemplo de valores
--------- | ------
versao | /v1, /v2
app-operation | pagamentos, boleto, transferencias, pix, doc, ted
app-action | bloquear e desbloquear

**sintaxe**:
```
/<versao>/<app-operation>[/<app-operation>][/<app-action>]
```

### Exemplo: Pagamento de Boletos
No contexto onde o cliente está identificado no HEADER 

Verbo | Recurso | Descrição
------|------|------
GET | /v1/pagamentos/boletos | retorna uma lista de de boletos do cliente *
POST | /v1/pagamentos/boletos | registra um boleto para pagamento online ou agendada
DELETE | /v1/pagamentos/boletos/{id} | permite excluir um agendamento de pagamento de boleto

* para mais detalhes sobre filtro ver detalhes de verbos HTTP

### Exemplo: Cartões
No contexto onde o cliente está identificado no HEADER 

Verbo | Recurso | Descrição
------|------|------
GET | /v1/cartoes | lista de cartões do cliente *
GET | /v1/cartoes/{id} | detalhes do cartão do cliente
GET | /v1/cartoes/{id}/faturas | lista de faturas do cliente *
GET | /v1/cartoes/{id}/faturas/{mes}/{ano} | retorna detalhe da fatura 
PATCH | /v1/cartoes/{id}/desbloquear | envia solicitação de desbloqueio do cartão
PATCH | /v1/cartoes/{id}/bloquear | envia solicitação de bloqueio do cartão

**Observação**: de acordo com a necessidade pode ser criada mais um sub derivação em app-operation, apenas em casos específicos utilizar app-action

## HTTP Header x QueryParam x PathParam

### HTTP Header (Todos Verbos HTTP)
Deve ser utilizado apenas para dados sensíveis de Segurança e Identificação que são se uso global do sistema que ficam disponíveis na aplicação.

**Devo usar para:**
* OAuth / JWT (Clains)
* ID-Client
* ID-Device

**Exemplo válidos**
```
'Accept': 'application/json',
'Content-Type': 'application/json'
'Authorization': 'Bearer ${JWT}'
'ID-Client': '99999999'
'ID-Device': '99999999'
```

**Nunca de usar para:**
* envio de parâmetros como filtro
* envio de dados para uso apenas no contexto daquele endpoint
* envio de dados de identificação do cliente que são protegidos pela LGPD

### PathParam (Todos Verbos HTTP)
Deve ser utilizado com moderação e apenas para ID de resources, em geral deve ser utilizado para identificar um resource

**Exemplo válidos**
```
/clientes/{id}
/clientes/{id}/enderecos
/clientes/{id}/enderecos/{id-endereco}
/clientes/{id}/faturas
/clientes/{id}/faturas/{id-fatura}
/clientes/{id}/faturas/{mes}/{ano}
```

**Nunca de usar para:**
* envio de parâmetros como filtro dinâmico e que representam muitos resources
* envio de dados sensíveis como CPF e CNPJ

### QueryParam (Verbo HTTP GET)
Deve ser utilizado para envio de dados que podem ou não ser obrigatórios mas que não são identificadores únicos

**Devo usar para:**
* Datas para uso em filtros
* Nomes
* CEP

**Exemplo válidos**
```
/clientes/filters?<param=valor>&<param=valor>&<param=valor>
/clientes/search?<param=valor>&<param=valor>
```

**Nunca de usar para:**
* envio de dados sensíveis como CPF, CNPJ, telefone, documentos pessoais, facebook account, ...
* nenhuma informação que possa identificar o usuário fora do escopo so sistema

