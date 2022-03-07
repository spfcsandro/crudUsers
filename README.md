Cadastro de Usuários (Estudo)

Fonte: Estudo do projeto do amigo Hernani Almeida (https://dev.to/2020nani/microservices-docker-e-tecnologias-de-mensageria-16jo?signin=true)

Criar uma aplicação utilizando tecnologias de mensageria (Kafka e fila(ActiveMq)) que são utilizadas para ligar aplicações independentes que se comunicam entre si, traduzindo Microservices :).

Essa aplicação consiste num cadastro de um Usuário que sera salvo em 3 tipos de database, ElasticSearch, Banco de memoria Redis e para finalizar em um database Sql Postgres. 

Para isso teremos 3 APIs (construídas utilizando arquitetura DDD) se comunicando entre si após a requisição do cadastro de um usuário realizada pelo front, vamos detalhar abaixo a função de cada API.

API de Acesso - Essa API ira receber a requisição de um cadastro de usuário e produzir uma mensagem em um tópico Kafka para que a mesma seja consumida pela aplicação seguinte.

API Orquestradora - Essa API recebe a mensagem produzida pela primeira API acima através de um Listener de um tópico KAFKA que estará captando as mensagem produzidas por este tópico. Apos receber a mensagem a API produz uma mensagem agora numa fila com os dados do usuário e após salva os dados deste usuário dentro do elasticsearch.

API ConsumerMq - Essa API recebe a mensagem produzida pela API acima através de um JmsListener e salva este usuário dentro de um banco de dados em memoria (Redis), estes usuarios serao listados no front para ser analisados por um admin e ser definido se valida ou não o cadastro, sendo validado será salvo em um banco de dados Postgres e excluído do banco de memorias Redis, caso seja invalido será excluído do banco de memorias Redis apenas.

Abaixo um simplex fluxograma da nossa aplicação:

![fluxo](https://user-images.githubusercontent.com/8027742/157108276-80bb774f-a72b-48fe-b94d-83a2d0861f9c.png)



#Java
#Spring Boot
#docker
#kafka
#ddd
#microservices
#Elasticsearch
#Kibana
#ActiveMQ
#PostgresSQL
#Redis
