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

kafka-avro-console-consumer \
--bootstrap-server kafka-1:9092, kafka-2:9092 \
--property schema.registry.url=http://schema-registry:8081 \
--from-beginning \
--topic shakespeare_years
