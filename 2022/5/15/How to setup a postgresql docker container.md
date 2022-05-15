# Set up a postgre database under docker

```bash
docker run --name postgreDatabase -p 5432:5432 -e POSTGRES_PASSWORD=12345DaLaoHu -d postgres
```

Now,

your username is: `postgres`

your password is: `12345DaLaoHu`

## For springboot, you may need
```bash
spring.datasource.url=jdbc:postgresql://localhost:5432/postgres
spring.datasource.username=postgres
spring.datasource.password=12345DaLaoHu
spring.datasource.driver-class-name=org.postgresql.Driver

spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.PostgreSQLDialect
spring.jpa.properties.hibernate.hbm2ddl.auto=create

```