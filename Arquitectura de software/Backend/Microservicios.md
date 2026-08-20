Cada capacidad se convierte en una aplicación independiente.

## FileSystem

```
organization-platform/
├── services/
│   ├── jobs-service/
│   │   └── src/
│   ├── users-service/
│   │   └── src/
│   ├── organization-chart-service/
│   │   └── src/
│   └── notification-service/
│       └── src/
├── packages/
│   └── contracts/
└── infrastructure/
```

Cada servicio puede tener su propia arquitectura interna:

```
jobs-service/
└── src/
    ├── domain/
    ├── application/
    ├── infrastructure/
    └── presentation/
```

Microservicios no reemplaza Clean Architecture. Responde otra pregunta:

- Clean Architecture: ¿cómo organizo el interior?
- Microservicios: ¿cómo divido y despliego el sistema?

NestJS puede crear servicios que procesan mensajes y eventos mediante transportes como RabbitMQ, Kafka, NATS o gRPC. [Documentación oficial de microservicios](https://docs.nestjs.com/microservices/basics).

## Cuándo utilizarlos

- Equipos independientes.
- Despliegues independientes.
- Escalabilidad muy diferente entre módulos.
- Límites de negocio claros.
- Necesidad comprobada de aislamiento.

## Desventajas

- Red, timeouts y reintentos.
- Consistencia distribuida.
- Duplicación de datos.
- Monitoreo complejo.
- Despliegues más costosos.
- Testing end-to-end difícil.
- Mucha infraestructura.

No recomendaría comenzar tu próximo proyecto con microservicios. Primero construye un buen monolito modular. Si los módulos tienen límites correctos, posteriormente podrás extraerlos.