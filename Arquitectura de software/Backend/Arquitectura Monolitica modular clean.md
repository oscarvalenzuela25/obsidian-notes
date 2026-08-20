
```
src/
└── features/
    └── comments/
        ├── presentation/
        │   ├── dto/
        │   │   ├── create-comment.request.dto.ts
        │   │   ├── update-comment.request.dto.ts
        │   │   └── comment.response.dto.ts
        │   ├── comments.controller.ts
        │   └── comments.routes.ts
        │
        ├── application/
        │   ├── use-cases/
        │   │   ├── create-comment.use-case.ts
        │   │   ├── get-comments.use-case.ts
        │   │   ├── update-comment.use-case.ts
        │   │   └── delete-comment.use-case.ts
        │   └── ports/
        │       └── comments.repository.ts
        │
        ├── domain/
        │   ├── entities/
        │   │   ├── comment.entity.ts
        │   │   ├── reply.entity.ts
        │   │   └── user.entity.ts
        │   └── errors/
        │       └── comment.errors.ts
        │
        └── infrastructure/
            └── persistence/
                └── sequelize/
                    ├── sequelize-comments.repository.ts
                    └── comment.persistence.mapper.ts
```

## Responsabilidad de cada carpeta

```
presentation/
```

Contiene todo lo relacionado con Express y HTTP:

- Rutas.
- Controladores.
- DTO de entrada.
- DTO de respuesta.
- Códigos HTTP.
- Lectura de `req.body`, `req.params` y `req.query`.

```
application/
```

Contiene las operaciones que puede realizar la aplicación:

- Crear comentario.
- Consultar comentarios.
- Actualizar comentario.
- Eliminar comentario.
- Contratos necesarios para ejecutar esas operaciones.

```
domain/
```

Contiene conceptos y reglas propias del negocio:

- Entidades.
- Errores de dominio.
- Comportamientos y validaciones del negocio.

```
infrastructure/
```

Contiene detalles técnicos reemplazables:

- Sequelize.
- Modelos de persistencia.
- Consultas.
- Implementaciones de repositorios.
- Mapeo entre persistencia y dominio.