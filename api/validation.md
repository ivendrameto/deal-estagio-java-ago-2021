# API - Validações com Bean Validation

[Voltar](./index.md)

1. Vamos adotar o modelo de validação de api rest com Bean Validation que prove um conjunto de validações já pré-definido.
2. Como definido na documentação de verbos http e erros uma falha de contrato irá gerar um HttpStatus 400 retornando uma lista de erros.

**Exemplo de REST**
```
@Operation(summary = "Atualiza versão app.")
@PutMapping("/{id}")
@ResponseStatus(HttpStatus.OK)
public VersaoDTO update(@PathVariable String id,
                                    @Valid @RequestBody VersaoDTO versaoDTO) {
    [implementação]
}
```
1. Anotamos o objeto que deve ser validado na assinatura do método rest com **@Valid**
2. O Objeto marcado para validação deve ser anotado de acordo com as validações necessárias

**Exemplo de Anotações**
* atributo não pode ser nulo.
```
@NotNull
private String nomeDoAtributo;
```

* atributo não pode ser nulo e vazio **" "** já não é vazio.
```
@NotEmpty
private String nomeDoAtributo;
```

* atributo não pode ser nulo e vazio **" "** já não é validado pois deve ser diferente branco.
```
@NotBlank
private String nomeDoAtributo;
```

* atributo deve ser nulo
```
@Null
private String nomeDoAtributo;
```

* atributo deve ser um e-mail (é preferível utilizar o @Pattern)
```
@Email
private String nomeDoAtributo;
```

* atributo deve ser numérico menor que o valor especificado.
```
@DecimalMax(value = "100.00", message = "{value}")
private BigDecimal nomeDoAtributo;
```

* atributo deve ser numérico maior que o valor especificado.
```
@DecimalMin(value = "100.00", message = "{value}")
private BigDecimal nomeDoAtributo;
```

* atributo deve ser um instância de tempo futuro.
```
@Future
private Date nomeDoAtributo;
```

* atributo deve ser um instância de tempo agora ou futuro.
```
@FutureOrPresent
private Date nomeDoAtributo;
```

* atributo deve ser um instância de tempo passado.
```
@Past
private Date nomeDoAtributo;
```

* atributo deve ser um instância de tempo agora ou passado.
```
@PastOrPresent
private Date nomeDoAtributo;
```

* atributo deve ser um numérico menor que o valor especificado.
```
@Max(value = 10L, message = "{value}")
private Long nomeDoAtributo;
```

* atributo deve ser um numérico maior que o valor especificado.
```
@Min(value = 10L, message = "{value}")
private Long nomeDoAtributo;
```

* atributo deve ser um numérico negativo.
```
@Negative
private BigDecimal nomeDoAtributo;
```

* atributo deve ser um numérico negativo ou zero.
```
@NegativeOrZero
private BigDecimal nomeDoAtributo;
```

* atributo deve ser um numérico positivo.
```
@Positive
private BigDecimal nomeDoAtributo;
```

* atributo deve ser um numérico positivo ou zero.
```
@PositiveOrZero
private BigDecimal nomeDoAtributo;
```

* atributo **Conjunto** deve numero de elementos conforme especificado.
```
@Size(min = 5, max = 10, message = "{min}/{max}")
private List<String> nomeDoAtributo;

@Size(min = 5, message = "{min}/{max}")
private List<String> nomeDoAtributo;
```

* atributo deve ser um conteúdo que corresponda a expressão regular.
```
@Pattern(regexp = ".+@.+\\.[a-z]+", message = "{regexp}")
private String nomeDoAtributo;
```

* atributo deve ser false.
```
@AssertFalse
private Boolean nomeDoAtributo;
```

* atributo deve ser true.
```
@AssertTrue
private Boolean nomeDoAtributo;
```