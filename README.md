create table years(id INTEGER PRIMARY KEY AUTOINCREMENT, name
VARCHAR(50), year INTEGER);
insert into years(name,year) values('Hamlet',1600);
insert into years(name,year) values('Julius Caesar',1599);
insert into years(name,year) values('Macbeth',1605);
insert into years(name,year) values('Merchant of Venice',1595);
insert into years(name,year) values('Othello',1604);
insert into years(name,year) values('Romeo and Juliette',1594);
insert into years(name,year) values('Anthony and Cleopatra',1606);



git clone --branch 5.3.0-v1.2.1 https://github.com/confluentinc/training-administration-src.git confluent-admin

kafka-avro-console-consumer --bootstrap-server kafka-1:9092, kafka-2:9092 --property schema.registry.url=http://schema-registry:8081 --from-beginning --topic shakespeare_years

curl -s -X POST -H "Content-Type: application/json" --data '{"name": "File-Sink-Connector","config": {"topics": "shakespeare_years","connector.class":"org.apache.kafka.connect.file.FileStreamSinkConnector","value.converter":"io.confluent.connect.avro.AvroConverter","value.converter.schema.registry.url":"http://schema-registry:8081","file": "data/test.sink.txt"}}' http://connect:8083/connectors

$ NS=io.confluent.monitoring.clients.interceptor && kafka-producer-perf-test --topic tune --num-records 10000000 --record-size 100 --throughput 1000 --producer-props bootstrap.servers=kafka-1:9092,kafka-2:9092 interceptor.classes=${NS}.MonitoringProducerInterceptor
