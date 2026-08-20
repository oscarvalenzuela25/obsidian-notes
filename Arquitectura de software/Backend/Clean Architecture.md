Clean Architecture busca que el negocio no dependa de Express, NestJS, Sequelize, Prisma ni otros detalles externos.

## FileSystem

```
src/
├── modules/
│   └── jobs/
│       ├── domain/
│       │   ├── entities/
│       │   │   └── job.entity.ts
│       │   ├── value-objects/
│       │   ├── services/
│       │   └── errors/
│       ├── application/
│       │   ├── use-cases/
│       │   │   └── add-job.use-case.ts
│       │   ├── ports/
│       │   │   └── job.repository.ts
│       │   └── commands/
│       │       └── add-job.command.ts
│       ├── infrastructure/
│       │   ├── persistence/
│       │   │   ├── sequelize-job.repository.ts
│       │   │   └── job.model.ts
│       │   └── mappers/
│       │       └── job.mapper.ts
│       ├── presentation/
│       │   └── http/
│       │       ├── jobs.controller.ts
│       │       └── dto/
│       │           └── create-job.request.dto.ts
│       └── jobs.module.ts
├── shared/
├── app.module.ts
└── main.ts
```

## Regla fundamental

```
Presentation ──┐
               ├──→ Application ──→ Domain
Infrastructure ┘
```

El centro no conoce las herramientas externas.

## Cuándo utilizarla

- Negocio complejo.
- Aplicaciones que vivirán varios años.
- Alta necesidad de testing.
- Varias formas de entrada: HTTP, colas, CLI, cron.
- Posibilidad real de cambiar infraestructura.
- Equipos grandes.

## Ventajas

- Casos de uso fáciles de probar.
- Dominio independiente del framework.
- Facilita cambiar persistencia.
- Responsabilidades claras.
- Mantiene controlada la complejidad.

## Desventajas

- Más archivos y abstracciones.
- Puede ser excesiva para un CRUD pequeño.
- Requiere comprender bien la regla de dependencias.
- Puede terminar en carpetas ceremoniales sin valor real.

Tu proyecto intenta aplicar esta arquitectura, pero todavía tiene dependencias desde `application` hacia implementaciones de `infrastructure`.