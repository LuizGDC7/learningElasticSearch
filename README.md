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

O Elasticsearch é um nó em um cluster. Em outras palavras, existem clusters, e nesses clusters, existem nós, cada nó é uma instância do Elasticsearch. Isso permite que dividamos os dados que estamos guardando. Um nó TEM um cluster, e vários nós pertencem a um cluster. Podemos ter mais de um cluster também.