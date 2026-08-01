MVC significa Model–View–Controller. En una API backend normalmente no existe una View HTML tradicional; la “vista” puede ser la respuesta JSON.

## FileSystem

```
src/
├── models/
│   └── job.model.ts
├── controllers/
│   └── job.controller.ts
├── routes/
│   └── job.routes.ts
├── services/
│   └── job.service.ts
├── middlewares/
└── app.ts
```

## Responsabilidades

- `Model`: datos, ORM y persistencia.
- `Controller`: recibe la petición y prepara la respuesta.
- `View`: JSON o plantilla HTML.
- `Service`: suele agregarse para evitar controladores enormes.

## Cuándo utilizarla

- APIs pequeñas.
- Aplicaciones renderizadas desde el servidor.
- Express con Sequelize o Mongoose.
- Proyectos donde la mayor parte del trabajo es CRUD.

## Ventajas

- Muy conocida.
- Fácil de implementar.
- Pocas abstracciones.
- Permite avanzar rápidamente.

## Desventajas

- MVC no indica dónde colocar reglas complejas.
- El modelo puede terminar mezclando persistencia y negocio.
- Los controladores o servicios suelen crecer demasiado.
- No establece una regla fuerte de dependencias.

MVC puede formar parte de una arquitectura mayor. Tu capa `presentation` contiene una variante de MVC, pero todo tu proyecto no es solamente MVC.