Cada operación o conjunto pequeño de operaciones se ejecuta como función.

## FileSystem

```
src/
├── functions/
│   ├── add-job/
│   │   ├── handler.ts
│   │   ├── schema.ts
│   │   └── use-case.ts
│   ├── update-job/
│   └── get-organization-chart/
├── domain/
├── infrastructure/
└── shared/
```

## Cuándo utilizarla

- Procesos esporádicos.
- Webhooks.
- Cron jobs.
- APIs con tráfico variable.
- Procesamiento de archivos.
- Integraciones pequeñas.

## Desventajas

- Cold starts.
- Límites de ejecución.
- Observabilidad distribuida.
- Desarrollo local más difícil.
- Puede fragmentar demasiado el negocio.

Serverless es principalmente una arquitectura de ejecución. Dentro de una función todavía puedes utilizar casos de uso, dominio y repositorios.