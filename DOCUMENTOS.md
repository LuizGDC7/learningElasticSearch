# Manipulação de Documentos

    Um documento não é nada mais do que a menor unidade de informação trabalhável do Elasticsearch, podemos ver eles de forma simplificada como Jsons salvos em um banco de dados não relacional.

## Índices

### Criação

``` Typescript
PUT /nome_indice
{
    "settings": {
        "number_of_shards": 2, 
        "number_of_replicas": 2 // 1 é o suficiente se aplicação não crítica, do contrário, >= 2 
    }
}
```

### Delação

```Typescript
DELETE /nome_indice
```

### Indexação de documentos

```Typescript

// Cria um documento novo mas sem ID dado por nós
POST /nome_indice/_doc
{
    "metadado1": dados,
    "metadado2": dados
}

// Cria documento mas com ID definido por nós
PUT /nome_indice/_doc/id
{
    "metadado1": dados,
    "metadado2": dados
}
```

## Recuperação

```Typescript
// Um documento
GET /nome_indice/id
```

## Alteração de documentos

Lembrando que documentos não são alterados, eles são copiados / alterados e novamente indexados, fica parecendo uma alteração, mas não é.

```Typescript
POST meu_indice/_update/id

"metadado": valor,
"metadado": {
    "metadado": valor
}

```

```Typescript

```