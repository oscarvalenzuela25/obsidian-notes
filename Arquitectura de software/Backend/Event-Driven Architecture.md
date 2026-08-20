Los módulos se comunican mediante eventos.

```
JobCreated
JobAssignedToTier
JobDeleted
OrganizationChartUpdated
```

## FileSystem

```
src/
├── modules/
│   └── jobs/
│       ├── application/
│       ├── domain/
│       │   └── events/
│       │       └── job-created.event.ts
│       └── infrastructure/
│           └── messaging/
│               └── job-event.publisher.ts
├── subscribers/
│   ├── notify-job-created.subscriber.ts
│   └── update-chart-cache.subscriber.ts
└── shared/
    └── messaging/
```

## Ejemplo

Al crear un cargo:

```
AddJobUseCase
    → guarda Job
    → publica JobCreated
        → actualiza caché
        → registra auditoría
        → envía notificación
```

## Cuándo utilizarla

- Procesos asíncronos.
- Integración entre módulos o servicios.
- Notificaciones.
- Auditoría.
- Tareas que no necesitan responder inmediatamente.
- Sistemas desacoplados.

## Desventajas

- Flujo más difícil de seguir.
- Manejo de reintentos e idempotencia.
- Eventos duplicados.
- Consistencia eventual.
- Necesidad de colas y observabilidad.

Para operaciones importantes que guardan en BD y publican eventos suele utilizarse el patrón Outbox, evitando guardar correctamente el Job pero perder el evento.