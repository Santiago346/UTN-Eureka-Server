# Eureka Server

Servidor de descubrimiento de servicios (Service Discovery) para la arquitectura de microservicios bancarios. Permite que `product-service` y `customer-service` se registren y se encuentren entre sí por nombre, sin necesidad de hardcodear IPs o puertos.

## Stack

- Spring Boot
- Spring Cloud Netflix Eureka Server
- Spring Cloud Config Client

## Configuración

`src/main/resources/application.yaml`:

```yaml
spring:
  application:
    name: eureka-server
  config:
    import: configserver:http://localhost:8888
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

Como el puerto y demás configuración de cada servicio vienen del Config Server, el orden correcto es:

1. Config Server
2. Eureka Server
3. product-service
4. customer-service

## Notas

- `register-with-eureka: false` y `fetch-registry: false` evitan que el propio Eureka Server intente registrarse a sí mismo como cliente.