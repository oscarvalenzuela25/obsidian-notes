Es probablemente la arquitectura backend más utilizada.

## FileSystem

```
src/
├── controllers/
│   └── job.controller.ts
├── services/
│   └── job.service.ts
├── repositories/
│   └── job.repository.ts
├── models/
│   └── job.model.ts
├── dto/
│   └── create-job.dto.ts
├── routes/
│   └── job.routes.ts
├── middlewares/
├── config/
└── app.ts
```

## Flujo

```
Route → Controller → Service → Repository → Database
```

## Ejemplo

```ts
class JobService {
  constructor(private readonly jobRepository: JobRepository) {}

  async addJob(input: CreateJobDto) {
    const nextTier = await this.jobRepository.findNextTier(input.tierId);

    return this.jobRepository.create({
      name: 'New Position',
      tierId: nextTier.id,
    });
  }
}
```

## Cuándo utilizarla

- APIs CRUD.
- Proyectos pequeños y medianos.
- Equipos que necesitan una estructura sencilla.
- MVP.
- Backoffice.
- Cuando el negocio todavía no tiene reglas complejas.

## Ventajas

- Fácil de aprender.
- Pocas carpetas.
- Flujo predecible.
- Se adapta perfectamente a Express y NestJS.
- Desarrollo rápido.

## Desventajas

- Los servicios pueden crecer demasiado.
- Se suelen mezclar reglas de negocio y base de datos.
- Las carpetas globales terminan con decenas de archivos.
- Cambiar el ORM puede afectar a los servicios.
- Los módulos no tienen límites muy claros.