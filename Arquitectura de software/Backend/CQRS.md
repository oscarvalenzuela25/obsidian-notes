CQRS separa las operaciones que modifican información de las que la consultan.

```
Commands → escriben
Queries  → leen
```

## FileSystem

```
src/
└── modules/
    └── jobs/
        ├── commands/
        │   ├── add-job.command.ts
        │   └── add-job.handler.ts
        ├── queries/
        │   ├── get-organization-chart.query.ts
        │   └── get-organization-chart.handler.ts
        ├── events/
        │   └── job-created.event.ts
        ├── domain/
        ├── infrastructure/
        └── jobs.module.ts
```

Ejemplo:

```
AddJobCommandHandler
    → valida reglas
    → escribe el Job
    → publica JobCreatedEvent

GetOrganizationChartQueryHandler
    → consulta una vista optimizada
    → devuelve directamente el gráfico
```

NestJS cuenta con soporte oficial para este patrón mediante `@nestjs/cqrs`, pero su propia documentación recomienda evaluarlo según la complejidad y escalabilidad requerida. [Documentación oficial de CQRS](https://docs.nestjs.com/recipes/cqrs).

## Cuándo utilizarlo

- Muchas reglas en las operaciones de escritura.
- Consultas muy diferentes al modelo de escritura.
- Auditoría.
- Gran diferencia entre cantidad de lecturas y escrituras.
- Procesamiento mediante eventos.

## Desventajas

- Más clases.
- Mayor complejidad.
- Posible consistencia eventual.
- Excesivo para un CRUD normal.