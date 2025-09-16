# learningElasticSearch
Repositório dedicado ao aprendizado de Banco de Dados não Relacional Elasticsearch

## O que é Elasticsearch

É uma engine de análise e busca textual 

Informações são salvas como documentos, que são a menor unidade de conhecimento com que conseguimos trabalhar no Elasticsearch, além disso, conseguimos trabalhar não apenas com recuperação de documentos, mas também com a análise da informação, usando algoritmos de machine learning.

## Elastic Stack

São as tecnologias usadas pelo elasticsearch para funcionar

### Kibana

Permite a visualização da informação armazenada. É como uma interface web para interagir com o elasticsearch, permite o uso de Dashboards (interfaces visuais que mostram informações relevantes, como o velocímetro de um carro), que mostrar informação definida por você.

### Logstash

Uma ferramenta originalmente dedicada ao monitoramente e registro de logs do elasticsearch. 

Hoje em dia, ela é mais completa, e funciona da seguinte forma: 

Entrada de dados / eventos;
Processamento; 
Envio de dados -> aqui o envio de dados pode ser feito usando várias plataformas, como e-mail, kafka, o próprio elasticsearch, endpoints, etc.

Stash é guardar ou esconder informação, em especial de forma segura.

### X-Pack

Adiciona funcionalidades ao elasticsearch. Algumas são:

Segurança;
Monitoramento;
Relatórios;
Alertas;
Comandos SQL;
Análise de grafos;
Machine Learning.

## Exemplos de arquitetura com o elasticsearch

### E-commerce

Banco de dados -> guardar dados;

Interface web -> interagir com o cliente;

Elasticsearch -> procurar por itens usando queries de texto, depois indo aos itens no banco de dados;

Kibana -> conseguiremos visualizar os dados;

MetricBeats -> poderemos pegar dados de picos de consumo de recursos computacionais e agir de acordo para prevenir erros ou saber quando aumentar a disponibilidade de recursos computacionais;

LogStash -> Faremos a ingestão de eventos e de logs, nos permitindo melhorar nosso sistema tanto a nível de código quanto a nível de usuários usando o sistema.

## Um pouco de teoria do funcionamento do Elasticsearch

### Engine

O Elasticsearch é um nó em um cluster. Em outras palavras, existem clusters, e nesses clusters, existem nós, cada nó é uma instância do Elasticsearch, ou seja, são engines de recuperação e análise de dados. Isso permite que dividamos os dados que estamos guardando. Um nó TEM um cluster, e vários nós pertencem a um cluster. Podemos ter mais de um cluster também.

### Sharding

Um nó é o espaço físico de armazenamento de informação.

Um índice nos permite acessar os nós.

O que acontece se tivermos 500 GB de documentos e tentarmos guardar eles em dois nós de 400 GB individualmente? Não vai caber em nenhum dos dois.

O que podemos fazer é dividir o índice em 2 shards, cada um com 250 GB, e guardamos esses documentos cada um em um nó. Assim conseguimos expandir horizontalmente a quantidade de documentos armazenada.

Shards também permitem paralelização na busca pela informação.

### Replication vs Snapshots

Replication é quando dados são copiados de um nó para outro, o ponto é permitir que caso um nó caie ou falhe, o acesso à informação se mantenha ativo. 

Snapshots são o backup em si, uma cópia de todos os dados em dado período de tempo. Serve para recuperar dados em graves crises, mas isso faz o sistema ficar off-line.

Então replication e snapshots atuam em ambientes distintos, Replication quer manter o acesso à informação mesmo com alguns percaussos, o Snapshot quer recuperar a informação completa em graves crises de perca de informação.