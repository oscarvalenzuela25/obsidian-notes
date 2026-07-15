Vertical Slice lleva la arquitectura por modulos un paso más allá.

En lugar de organizar solamente por `products`, divides el módulo por **casos de uso completos**.

```
src/
├── features/
│   ├── products/
│   │   ├── list-products/
│   │   │   ├── ListProductsPage.tsx
│   │   │   ├── ProductList.tsx
│   │   │   ├── useListProducts.ts
│   │   │   ├── listProducts.api.ts
│   │   │   ├── listProducts.types.ts
│   │   │   └── index.ts
│   │   ├── create-product/
│   │   │   ├── CreateProductPage.tsx
│   │   │   ├── ProductForm.tsx
│   │   │   ├── useCreateProduct.ts
│   │   │   ├── createProduct.api.ts
│   │   │   ├── createProduct.schema.ts
│   │   │   └── index.ts
│   │   └── edit-product/
│   └── users/
│       ├── list-users/
│       ├── create-user/
│       └── edit-user/
└── shared/
```

## Diferencia con la arquitectura modular

Modular:

```
products/
├── components/
├── hooks/
├── pages/
└── api/
```

Vertical Slice:

```
products/
├── list-products/
├── create-product/
├── update-product/
└── delete-product/
```

Cada slice contiene todo lo necesario para completar una acción.

## Ejemplo real

Para crear productos solo necesitas revisar:

```
features/products/create-product/
```

Ahí encuentras:

- Formulario.
- Validaciones.
- Tipos.
- Hook.
- Petición.
- Página.
- Tests.

## Ventajas

Tiene una alta cohesión: todo lo relacionado con un caso de uso permanece junto.

También evita que aparezcan carpetas enormes como:

```
components/
hooks/
services/
```

## Problemas

Puede duplicar componentes o tipos si no se establecen reglas claras.

Por ejemplo, `ProductCard` podría utilizarse tanto en listado como en favoritos. En ese caso debe subir a un nivel compartido dentro del dominio:

```
features/products/shared/
└── ProductCard/
```

O convertirse en una entidad reutilizable.

## Cuándo usarla

Módulos grandes con muchos casos de uso. Es especialmente buena cuando el equipo trabaja por historias o tickets:

```
HU-203: Crear producto
HU-204: Editar producto
HU-205: Desactivar producto
```