# API : Verbos HTTP seus Status de retorno

[Voltar](./index.md)

## Utilização em CRUD
Verbo | URN | Body | Descrição
----- | --- | ---- | ------
GET | / | sim | recupera lista de dados
GET | /{id} | sim | retorna o detalhes um registro
POST | / | sim | cria um registro
PUT | /{id} | sim | atualiza todo o registro
PATCH | /{id} | sim | atualiza parte do registro
DELETE | /{id} | não | remove um registro

### Recomendação : GET /
**Observação**: trazer um implementação de filtros dinâmicos com Specification e Query/Critetia para os services.

**Não usar**
```
@Operation(summary = "Retorna uma versão atual e mínima do aplicativo.")
@GetMapping(value = "")
@ResponseStatus(HttpStatus.OK)
public List<VersaoDTO> get() {
        [implementação de consulta]
    return .....
}
```
**Usar**
```
@Operation(summary = "Retorna uma versão atual e mínima do aplicativo.")
@GetMapping(value = "")
@ResponseStatus(HttpStatus.OK)
public PageResponseDTO<VersaoDTO> get(@RequestParam(value = "page", defaultValue = "0") int page,
                                      @RequestParam(value = "size", defaultValue = "30") int size,
                                      @RequestParam Map<String,String> allParams) {
        [implementação de consulta]
    return .....
}
```

## HTTP - Status de retorno

### Sucessos
Verbo | Body | HTTP Status
----- | ----- | ----- 
DELETE | não | 204
GET | sim | 200
POST | sim | 201
PUT | sim | 200
PATCH | sim | 200

### Erros
**Erros referentes exceptions são tratados por Handlers pré-definidos**
Erros/Exceptions | HTTP Status
-----------------|-------------
Falhas de infra-estrutura na app de entrada | 500 
Falhas de infra-estrutura na app de chamada (timeout) | 504 
Falhas configuração API URI não existe | 404
Falhas segurança não logado | 401
Falhas segurança logado mas sem permissões | 403

**Erros de Negócio**
Erros/Exceptions | HTTP Status | Descrição
-----------------|-------------|-------------
Falha de contrato na da API | 400 | utilizando om conceito de BeanValidation na API podemos unificar esse comportamento
Falha de negócio | 422 | erros negociais que devem retornar uma mensagem especifica.

## Retornos possíveis
**Observação**: 
* criar filtro de dados no ExceptionHandler baseado no profile da aplicação para reduzir os dados exibidos em produção.
* incluir na mensagem um UUID para facilitar a analise de logs.
```
{
    "path" : "/v1/...",
    "status": 401,
    "timestamp": 1111111111,
    "numberOfErrors" : 1,
    "errors": [
        {
            "codigo": "VAL-0000",
            "mensagem": "Incorrect username or password.",
            "detalhe": "Authentication failed due to incorrect username or password."
        }
    ]
}
```