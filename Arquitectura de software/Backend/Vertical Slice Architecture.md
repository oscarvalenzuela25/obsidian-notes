En lugar de organizar por tipo técnico, organiza cada operación completa.

## FileSystem

```
src/
└── features/
    └── jobs/
        ├── add-job/
        │   ├── add-job.route.ts
        │   ├── add-job.controller.ts
        │   ├── add-job.handler.ts
        │   ├── add-job.schema.ts
        │   └── add-job.test.ts
        ├── update-job/
        │   ├── update-job.controller.ts
        │   ├── update-job.handler.ts
        │   └── update-job.schema.ts
        ├── delete-job/
        └── get-jobs/
```

Cada carpeta contiene todo lo necesario para una funcionalidad.

## Flujo

```
POST /jobs → AddJobHandler → Database
PUT /jobs/:id → UpdateJobHandler → Database
```

No es obligatorio que todas las operaciones pasen por un `JobService` gigante.

## Cuándo utilizarla

- Muchas funcionalidades independientes.
- Equipos trabajando en paralelo.
- Aplicaciones con casos de uso claros.
- CQRS.
- Sistemas donde los servicios tradicionales comienzan a crecer demasiado.

## Ventajas

- Alta cohesión.
- Todo lo relacionado con una operación está junto.
- Fácil eliminar o modificar una funcionalidad.
- Reduce los servicios de miles de líneas.
- Los tests quedan cerca del comportamiento.

## Desventajas

- Puede duplicar pequeñas utilidades.
- Aumenta el número de carpetas.
- Si se aplica sin reglas, cada slice puede funcionar de manera diferente.
- No siempre vale la pena para un CRUD pequeño.

Es similar a cómo organizas tu frontend por features, pero llevándolo al nivel de cada caso de uso.