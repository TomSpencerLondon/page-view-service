# page-view-service

Run:
```bash
mvn clean package
```

To create docker image run:
```bash
 mvn clean package docker:build
```

### Run docker images on same network:

```bash
docker network create pageview

docker run --name mysqldb --network pageview -p 3306:3306 -e MYSQL_DATABASE=pageviewservice -e MYSQL_ALLOW_EMPTY_PASSWORD=yes -d mysql

docker run -d --name rabbitmq --network pageview -p 8081:15672 -p 5671:5671 -p 5672:5672 rabbitmq:3-management

docker run --name pageviewservice -p 8082:8081 \
--network pageview \
springframeworkguru/pageviewservice
```

### Add correct connection configuration to application.properties

```bash
server.port=8082

spring.datasource.url=jdbc:mysql://mysqldb/pageviewservice
spring.datasource.username=root

spring.jpa.show-sql=true
spring.jpa.hibernate.ddl-auto=update
spring.jpa.hibernate.naming.implicit-strategy=org.hibernate.boot.model.naming.ImplicitNamingStrategyLegacyHbmImpl
spring.jpa.hibernate.naming.physical-strategy=org.springframework.boot.orm.jpa.hibernate.SpringPhysicalNamingStrategy
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL5Dialect

# RabbitMQ
spring.rabbitmq.host=rabbitmq
```

### Receive messages from rabbitmq broker

```bash
pageviewservice> Got Message!
pageviewservice> <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
pageviewservice> <pageViewEvent>
pageviewservice>     <correlationId>51fd2637-295e-415a-b5c4-6b6c6c764b65</correlationId>
pageviewservice>     <pageUrl>springfarmework.guru/product/4</pageUrl>
pageviewservice>     <pageViewDate>2023-03-15T18:31:09.774Z</pageViewDate>
pageviewservice> </pageViewEvent>
```


