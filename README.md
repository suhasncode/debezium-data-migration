# debezium-data-migration
Migrating data using Debezium connectors on Kafka

# Installation Steps:
- Install postgre-src-db
- Install postgre-dst-db
- Install mysql-dst-db
- Install zookeeper
- Install Kafka-1
- Install Kafka-2
- Install kafdrop
- Install kconnect
- Install Kafka-connect-ui
- Install schema-registry


Create Source Connector with this config:
---------------------------------------------------------------------------
connector.class=io.debezium.connector.postgresql.PostgresConnector
database.dbname=postgres
database.user=postgres
tasks.max=1
database.port=5432
plugin.name=pgoutput
key.converter.schemas.enable=true
value.converter.schema.registry.url=http://schema-registry:8081
topic.prefix=postgressql
database.hostname=postgre-src-db
database.password=adfadv32cbbs4$#se1
poll.interval.ms=3000
value.converter.schemas.enable=true
value.converter=io.confluent.connect.avro.AvroConverter
key.converter=io.confluent.connect.avro.AvroConverter
key.converter.schema.registry.url=http://schema-registry:8081
snapshot.mode=initial

Create Sink for MySQL:
---------------------------------------------------------------------------
connector.class=io.debezium.connector.jdbc.JdbcSinkConnector
table.name.format=tab1
connection.password=wohvaflafsdih2q33@fgg4
primary.key.mode=record_key
topics=postgressql.public.tab1
tasks.max=1
connection.username=root
value.converter.schema.registry.url=http://schema-registry:8081
delete.enabled=true
schema.evolution=basic
connection.url=jdbc:mysql://mysql-dst-db:3306/repl_db
value.converter=io.confluent.connect.avro.AvroConverter
key.converter=io.confluent.connect.avro.AvroConverter
key.converter.schema.registry.url=http://schema-registry:8081

OR

{
  "connector.class": "io.debezium.connector.jdbc.JdbcSinkConnector",
  "table.name.format": "tab1",
  "connection.password": "wohvaflafsdih2q33@fgg4",
  "primary.key.mode": "record_key",
  "topics": "postgressql.public.tab1",
  "tasks.max": "1",
  "connection.username": "root",
  "value.converter.schema.registry.url": "http://schema-registry:8081",
  "delete.enabled": "true",
  "schema.evolution": "basic",
  "connection.url": "jdbc:mysql://mysql-dst-db:3306/repl_db",
  "value.converter": "io.confluent.connect.avro.AvroConverter",
  "key.converter": "io.confluent.connect.avro.AvroConverter",
  "key.converter.schema.registry.url": "http://schema-registry:8081"
}

Create Sink for Postgres:
---------------------------------------------------------------------------
connector.class=io.debezium.connector.jdbc.JdbcSinkConnector
errors.log.include.messages=true
connection.password=adfadv32cbbs4$#se1
primary.key.mode=record_key
topics=postgressql.public.tab1
tasks.max=1
connection.username=postgres
value.converter.schema.registry.url=http://schema-registry:8081
delete.enabled=true
schema.evolution=basic
value.converter=io.confluent.connect.avro.AvroConverter
connection.url=jdbc:postgresql://postgre-dst-db:5432/postgres
errors.log.enable=true
insert.mode=upsert
key.converter=io.confluent.connect.avro.AvroConverter
key.converter.schema.registry.url=http://schema-registry:8081

OR

{
  "connector.class": "io.debezium.connector.jdbc.JdbcSinkConnector",
  "errors.log.include.messages": "true",
  "connection.password": "adfadv32cbbs4$#se1",
  "primary.key.mode": "record_key",
  "topics": "postgressql.public.tab1",
  "tasks.max": "1",
  "connection.username": "postgres",
  "value.converter.schema.registry.url": "http://schema-registry:8081",
  "delete.enabled": "true",
  "schema.evolution": "basic",
  "value.converter": "io.confluent.connect.avro.AvroConverter",
  "connection.url": "jdbc:postgresql://postgre-dst-db:5432/postgres",
  "errors.log.enable": "true",
  "insert.mode": "upsert",
  "key.converter": "io.confluent.connect.avro.AvroConverter",
  "key.converter.schema.registry.url": "http://schema-registry:8081"
}

