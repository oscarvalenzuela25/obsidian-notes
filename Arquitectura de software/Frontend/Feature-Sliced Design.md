Feature-Sliced Design, normalmente llamado FSD, propone capas específicas para aplicaciones frontend.

```
src/
├── app/
├── pages/
├── widgets/
├── features/
├── entities/
└── shared/
```

La regla general de dependencias es:

```
app
 ↓
pages
 ↓
widgets
 ↓
features
 ↓
entities
 ↓
shared
```

Una capa inferior no debería importar una superior.

## Estructura aplicada a tu caso

```
src/
├── app/
│   ├── providers/
│   ├── router/
│   ├── layouts/
│   ├── store/
│   ├── i18n/
│   └── styles/
├── pages/
│   ├── users/
│   │   └── UsersPage.tsx
│   ├── products/
│   │   └── ProductsPage.tsx
│   └── product-detail/
│       └── ProductDetailPage.tsx
├── widgets/
│   ├── topbar/
│   ├── user-table/
│   └── product-grid/
├── features/
│   ├── create-user/
│   ├── edit-user/
│   ├── create-product/
│   ├── search-products/
│   └── change-language/
├── entities/
│   ├── user/
│   │   ├── api/
│   │   ├── model/
│   │   ├── ui/
│   │   └── index.ts
│   └── product/
│       ├── api/
│       ├── model/
│       ├── ui/
│       └── index.ts
└── shared/
    ├── api/
    ├── ui/
    ├── lib/
    ├── config/
    └── types/
```

## Qué representa cada capa

### `shared`

Código que no conoce el negocio.

```
shared/
├── ui/Button/
├── api/httpClient.ts
├── lib/formatCurrency.ts
├── lib/getErrorMessage.ts
└── types/pagination.ts
```

### `entities`

Conceptos principales del dominio.

```
entities/product/
├── api/products.api.ts
├── model/product.types.ts
├── model/product.store.ts
├── ui/ProductCard.tsx
└── index.ts
```

### `features`

Acciones que realiza el usuario.

```
features/create-product/
features/change-language/
features/deactivate-user/
```

### `widgets`

Bloques grandes formados por entidades y features.

```
widgets/product-table/
widgets/topbar/
widgets/user-profile-panel/
```

### `pages`

Composición final de una ruta.

### `app`

Configuración global, router, providers, layouts y estilos base.

## Ventajas

Tiene reglas explícitas y escala muy bien en proyectos grandes.

## Problemas

Puede ser excesiva para una aplicación pequeña. También requiere que todo el equipo entienda bien la diferencia entre:

- Entity.
- Feature.
- Widget.
- Page.

Para tu caso puede ser útil, pero no empezaría con todas sus capas desde el primer día.