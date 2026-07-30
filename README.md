# Eureka Server

Servidor de descubrimiento de servicios (Service Discovery) para la arquitectura de microservicios bancarios. Permite que `product-service` y `customer-service` se registren y se encuentren entre sí por nombre, sin necesidad de hardcodear IPs o puertos.

## Stack

- Spring Boot
- Spring Cloud Netflix Eureka Server

## Configuración

`src/main/resources/application.yml`:

```yaml
server:
  port: 8761

eureka:
  client:
    register-with-eureka: false
    fetch-registry: false
  instance:
    hostname: localhost
```

## Cómo correrlo

```bash
mvn spring-boot:run
```

El servidor levanta en el puerto **8761**.

## Dashboard

Una vez levantado, se puede ver el estado de los servicios registrados en:

```
http://localhost:8761
```

## Orden de arranque

Este servicio debe levantarse **primero**, antes que el Config Server y los microservicios (`product-service`, `customer-service`), ya que estos dependen de que Eureka esté disponible para registrarse.

## Notas

- `register-with-eureka: false` y `fetch-registry: false` evitan que el propio Eureka Server intente registrarse a sí mismo como cliente.
- No depende del Config Server — arranca de forma completamente independiente con su configuración local.