También se conoce como Ports and Adapters.

La aplicación define puertos; las herramientas externas implementan adaptadores.

## FileSystem

```
src/
└── jobs/
    ├── core/
    │   ├── domain/
    │   │   └── job.entity.ts
    │   ├── use-cases/
    │   │   └── add-job.use-case.ts
    │   └── ports/
    │       ├── in/
    │       │   └── add-job.port.ts
    │       └── out/
    │           └── job.repository.port.ts
    └── adapters/
        ├── in/
        │   └── http/
        │       └── jobs.controller.ts
        └── out/
            ├── persistence/
            │   └── sequelize-job.repository.ts
            └── events/
                └── rabbitmq-job.publisher.ts
```

## Ejemplo mental

La aplicación es un enchufe.

El puerto dice:

``` ts
interface JobRepository {
  save(job: Job): Promise<Job>;
}
```

Los adaptadores posibles son:

```
SequelizeJobRepository
PrismaJobRepository
InMemoryJobRepository
DynamoJobRepository
```

El caso de uso solo conoce el enchufe, no el aparato conectado.

## Cuándo utilizarla

Prácticamente los mismos casos que Clean Architecture:

- Múltiples integraciones.
- Base de datos, caché, colas y APIs.
- Tests aislados.
- Negocio importante.
- Aplicación independiente de herramientas.

## Ventajas

- Hace explícitas las entradas y salidas.
- Excelente testabilidad.
- Adaptable a HTTP, GraphQL, colas y CLI.
- Facilita reemplazar integraciones.

## Desventajas

- Muchos contratos.
- Puede generar abstracciones innecesarias.
- El concepto de puerto/adaptador puede costar al principio.

Tu controlador es un adaptador de entrada. Tu repositorio y datasource son adaptadores de salida.