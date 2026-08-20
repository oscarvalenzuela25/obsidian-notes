Esta es una de las mejores opciones para comenzar un backend que pueda escalar.

La aplicación se despliega como una sola unidad, pero internamente está dividida en módulos de negocio.

## FileSystem

```
src/
├── modules/
│   ├── jobs/
│   │   ├── jobs.controller.ts
│   │   ├── jobs.service.ts
│   │   ├── jobs.repository.ts
│   │   ├── job.entity.ts
│   │   ├── dto/
│   │   └── jobs.module.ts
│   ├── users/
│   ├── tiers/
│   └── divisions/
├── shared/
├── config/
├── app.module.ts
└── main.ts
```

## Idea principal

Cada módulo controla una capacidad del negocio:

```
JobsModule
UsersModule
TiersModule
DivisionsModule
```

Un módulo no debería entrar directamente a las tablas o archivos internos de otro. Debería utilizar:

- Una API pública del módulo.
- Un servicio exportado.
- Un caso de uso.
- Un evento.
- Un contrato explícito.

## Cuándo utilizarla

- Casi cualquier proyecto nuevo.
- Equipos pequeños o medianos.
- Aplicaciones que podrían crecer.
- Cuando aún no se justifican microservicios.
- SaaS, e-commerce, sistemas empresariales y APIs.

## Ventajas

- Modularidad sin complejidad distribuida.
- Un solo despliegue.
- Transacciones de BD sencillas.
- Menos infraestructura.
- Puede evolucionar a microservicios.
- Encaja naturalmente con los módulos de NestJS.

## Desventajas

- Los límites pueden romperse fácilmente.
- Todo se despliega junto.
- Una falla grave puede afectar toda la aplicación.
- Requiere disciplina para no crear dependencias circulares.

Tu proyecto ya es un monolito modular básico.