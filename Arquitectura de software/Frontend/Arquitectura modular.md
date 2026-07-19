
```
src/
├── app/
│   ├── router/
│   ├── layouts/
│   ├── providers/
│   └── App.tsx
├── features/
│   ├── users/
│   │   ├── components/
│   │   ├── pages/
│   │   ├── hooks/
│   │   ├── api/
│   │   ├── store/
│   │   ├── types/
│   │   └── index.ts
│   └── products/
│       ├── components/
│       ├── pages/
│       ├── hooks/
│       ├── api/
│       ├── store/
│       ├── types/
│       └── index.ts
└── shared/
    ├── components/
    ├── api/
    ├── i18n/
    ├── utils/
    └── types/
```

A veces en ves de tener app o shared, todas las carpetas que tienen esos 2 modulos estan en el nivel de features o modules, dando a entender que lo que esta al mismo nivel es lo que se comparte y lo que esta en features o modules vive en su mundo.
## Cómo funciona

Cada módulo contiene todo lo relacionado con su dominio.

```
features/products/
├── api/
│   └── products.api.ts
├── components/
│   ├── ProductCard.tsx
│   └── ProductCard.styles.ts
├── hooks/
│   └── useProducts.ts
├── pages/
│   ├── ProductsPage.tsx
│   └── ProductDetailPage.tsx
├── store/
│   └── products.store.ts
├── types/
│   └── product.types.ts
└── index.ts
```

Cuando trabajas en productos, casi todo está dentro de `features/products`.

## Ventajas

- Fácil de escalar.
- Los módulos tienen límites claros.
- Es sencillo eliminar o mover una funcionalidad.
- Distintos desarrolladores pueden trabajar en módulos diferentes.
- Encaja muy bien con React.

## Riesgo

Dentro de cada feature puedes terminar recreando una arquitectura por tipos:

```
components/
hooks/
services/
types/
stores/
```

Eso no es necesariamente malo, pero cuando el módulo crece mucho comienza a pasar el mismo problema a menor escala.

## Cuándo usarla

Es una excelente arquitectura general para una SPA mediana o grande.