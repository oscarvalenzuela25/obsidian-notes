Microfrontends divide el frontend en aplicaciones independientes.

```
apps/
├── shell/
├── users-app/
├── products-app/
└── shared-ui/

packages/
├── design-system/
├── api-client/
├── auth/
└── types/
```

Ejemplo con Module Federation:

```
shell
├── carga users-app
└── carga products-app
```

Cada aplicación puede tener su propio:

- Router.
- Estado.
- Pipeline.
- Equipo.
- Despliegue.

## Ventajas

Permite que distintos equipos trabajen y desplieguen independientemente.

## Problemas

Introduce complejidad en:

- Autenticación.
- Estado compartido.
- Navegación.
- Versiones.
- Estilos.
- Rendimiento.
- Testing integrado.

Tener dos módulos, `users` y `products`, no justifica microfrontends. Primero conviene construir un **monolito modular**.