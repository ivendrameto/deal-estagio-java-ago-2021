# API - Padrões de nomes 

[Voltar](./index.md)

## Premissas
* APIs exposta devem identificar origem e versão

## Nome do recurso api/rotas
* Evitar nomes compostos, caso não seja viável a troca, utilizar conceito de slug name na definição do recurso.
* Apenas letras minúsculas e utilizando '-' no lugar dos espaços

**Exemplos**
```
Pagamentos ........: /pagamentos/
Gerar Documentos ..: /gerar-documentos/
Pagar contas ......: /pagar-contas/
```

## Itens de payload
Objetos que representam entradas e saídas de API/Rotas devem utilizar padrão de nomes de atributos java utilizando camelCase.
