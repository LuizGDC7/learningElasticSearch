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

### Deleção

```Typescript
DELETE /nome_indice
```

Deleção por query

```Typescript
POST /nome_indice/_delete_by_query
{
    "query": {
        "match_all": {}
    }
}
```
### Indexação de documentos

```Typescript

// Cria um documento novo mas sem ID dado por nós
POST /nome_indice/_doc
{
    "metadado1": dados,
    "metadado2": dados
}

// Cria documento mas com ID definido por nós, também substitui o documento se já existe
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
    Alteração com query:

```Typescript
// Ou seja  aplicamos a query e depois a script score, é inteligente
POST /nome_indice_update_by_query
{
    "script": {
        "source": "ctx._source.in_stock--"
    },
    "query": {
        "match_all": {}
    }
}

``` 


Manipulação scriptada

Para fazer isso, usamos o "script" do elasticsearch. Podemos passar parâmetros, verificar atributos, etc, exemplo:


```Typescript
PUT /my-index/_doc/7
{
  "nome": "Alagoas",
  "pessoas": 575
}

POST /my-index/_update/7
{
    "script": {
      "source": """
        if(ctx._source.pessoas >= 0){
          ctx._source.pessoas--;
        }else{
          ctx.op = 'noop';
        }
      """ 
    } 
}

```

### Upserts

São basicamente alterações da seguinte lógica:

    if(doc_existe){
        alterar_doc();
    }else{
        criar_doc();
    }

```Typescript

// Ou seja, existe? Incrementa no stock, não existe? Cria 
POST /nome_indice/_update/id
{
    "script": {
        "source": "ctx._source.in_stock++"
    },
    "upsert": {
        "name": "Blender",
        "price": 399,
        "in_stock": 5
    }
}
```

## Deleção

Não tem segredo, é só usar a comunicação DELETE:

```Typescript
DELETE /nome_indice/_doc/id
```

## BULK API

Nos permite fazer operações em lotes de documentos

O formato é mais ou menos o seguinte em NDJSON

    action_and_metadata\n
        optional_source\n
    action_and_metadata\n
        optional_source\n

```Typescript
POST /nome_indice/_bulk ou /_bulk para vários índices
// vários índices

{"index": {"_index": "nome_indice", "_id": 200}}
{"name": "Espresso Machine", "price": 199, "in_stock": 5}
{"index": {"_index": "nome_indice", "_id": 201}}
{"name": "Banana", "price": 5, "in_stock": 20}

// Único índice

{"update": {"_id": 200}}
{"doc": {"in_stock": 10}}
{"delete": {"_id": 201}}


// LEMBRE-SE DE TERMINAR COM UMA LINHA VAZIA
```


```Typescript

```