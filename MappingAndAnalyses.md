# Mapping and Analysis

## Analysis

Permite que processemos os textos de forma eficiente

### Analyzer

Uma pipeline de processamento de texto, composta por 3 partes:

    Filtro de caracteres -> Adiciona, remove, altera caracteres

    Tokenizer -> apenas um por analyzer, o tokenizer divide a string em tokens

    Filtro de tokens -> consegue adicionar, remover ou alterar tokens 

### API

```Typescript
POST /_analyze
{
"text": "2 guys walk into  a bar, but the third... DUCKS! :-)",
"analyzer": "standard"
}
```
```Typescript
POST /_analyze
{
"text": "2 guys walk into  a bar, but the third... DUCKS! :-)",
"char_filter": [],
"analyzer": "standard",
"filter": ["lowercase"]
}
```

## Mapping

Basicamente, definimos um schema para nossa base de dados não relacional. Não é necessário explicitar os metadados no mapping para que eles sejam indexados, pois se um metadado não existir, o elasticsearch cria um na hora.

### Coerção

Quando indexando dados, se você fizer o schema com um tipo de dados e alimentar uma string ao invés de um float, o elasticsearch converte a string pra float (se possível).

Alguns problemas surgem:

O valor indexado não é o mesmo que o valor no _source, esse valor é o primeiro valor fornecido, então se vocÊ fornecer o primeiro valor errado, o dado no _source fica de tipo errado. A indexação tem os tipos corretos, o problema é o _source, ou seja, se você for pegar esse dado para trabalhar depois.

Em resumo, a busca pelos dados não é prejudicada, mas o uso dos dados posteriormente. 

Se você usar mapeamento dinâmico (ou seja, não fornecer schema e ir adicionando metadados), coerção não funciona.

Se você não quiser problemas, garanta que está fornecendo os tipos corretos.

## Mapping - Mapeamento explícito

```Typescript
PUT /nome_indice
{
    "mappings": {
        "properties": {
            "rating": {
                "type": "float"
            },
            "content": {
                "type": "text"
            },
            "product_id": {
                "type": "integer"
            },
            "author": { // Isso é um objeto não nested
                "properties":{
                    "firts_name": {"type": "text"},
                    "last_name": {"type": "text"},
                    "email": {"type": "keyword"}
                }
            }
        }
    }
}
```

Para saber qual é o mapeamento sendo usado, podemos fazer:

````Typescript
GET /nome_indice/_mapping

// Podemos pegar mais coisas também, adicionando o item de interesse no cabeçalho de requisição
```

## Mapping - Tipos de Dados

### Keywords

Para match exato, serve para texto que não muda e está estruturado, por exemplo, e-mails. É analizado com o keyword analyzer, que literalmente não mexe na string.

### Arrays

Não tem mapeamento, todo metadado no elasticsearch pode receber 0 ou mais itens, simplesmente entregue para ele um array a ser indexado.

A exigência é que os tipos de dados sejam iguais. A menos que a coerção de dados dos dados de tipo "errado" sejam possíveis.

Elasticsearch achata arrays, então algo como

```Typescript
[0, 1, [2, 3], 5] 

// Vira

[0, 1, 2, 3, 5]
```

Se você quiser que a estrutura se mantenha, vai precisar usar o parâmetro nested.
```Typescript

```