Es la estructura más sencilla y suele aparecer en proyectos React pequeños.
Ejemplo de file system
```
src/
├── components/
│   ├── Button.tsx
│   ├── UserCard.tsx
│   └── ProductCard.tsx
├── pages/
│   ├── UsersPage.tsx
│   └── ProductsPage.tsx
├── hooks/
│   ├── useUsers.ts
│   └── useProducts.ts
├── stores/
│   ├── settings.store.ts
│   ├── users.store.ts
│   └── products.store.ts
├── services/
│   ├── users.service.ts
│   └── products.service.ts
├── types/
│   ├── user.types.ts
│   └── product.types.ts
├── layouts/
├── styles/
├── utils/
├── locales/
└── config/
    └── axios.ts
```
## Ventajas

Es fácil de entender al comenzar y funciona bien para proyectos pequeños.
## Problemas

Cuando necesitas modificar productos, probablemente debes abrir:

```
pages/ProductsPage.tsx
components/ProductCard.tsx
hooks/useProducts.ts
stores/products.store.ts
services/products.service.ts
types/product.types.ts
```

El código relacionado con productos queda disperso por toda la aplicación.

## Cuándo usarla

Prototipos, aplicaciones pequeñas o proyectos con pocas pantallas.