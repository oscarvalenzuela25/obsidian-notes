La arquitectura por capas separa el código según su responsabilidad.

```
src/
├── presentation/
│   ├── components/
│   ├── pages/
│   ├── layouts/
│   └── styles/
├── application/
│   ├── hooks/
│   ├── stores/
│   └── use-cases/
├── domain/
│   ├── models/
│   ├── rules/
│   └── repositories/
├── infrastructure/
│   ├── http/
│   ├── repositories/
│   └── storage/
└── shared/
    ├── i18n/
    ├── utils/
    └── types/
```

La dirección habitual de dependencias es:

```
presentation
      ↓
application
      ↓
domain
      ↑
infrastructure
```

## Ejemplo

La página de productos no utiliza Axios directamente.

```
ProductsPage
    ↓
useProducts
    ↓
GetProductsUseCase
    ↓
ProductsRepository
    ↓
AxiosProductsRepository
```

## Ventajas

Separa muy bien la interfaz, la lógica y la infraestructura. También facilita reemplazar Axios, Zustand o una API.

## Problema principal

Los módulos vuelven a quedar dispersos:

```
presentation/pages/products/
application/use-cases/products/
domain/models/product/
infrastructure/repositories/products/
```

Es ordenada técnicamente, pero no siempre resulta cómoda para trabajar por funcionalidades.

## Cuándo usarla

Aplicaciones con reglas de negocio importantes, varios orígenes de datos o alta necesidad de testing.