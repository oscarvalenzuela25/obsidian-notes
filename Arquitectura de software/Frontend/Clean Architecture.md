Clean Architecture busca que la lógica importante no dependa directamente de React, Axios, Zustand o el navegador.

```
src/
├── domain/
│   ├── entities/
│   │   ├── User.ts
│   │   └── Product.ts
│   ├── repositories/
│   │   ├── UserRepository.ts
│   │   └── ProductRepository.ts
│   └── errors/
├── application/
│   ├── use-cases/
│   │   ├── GetProducts.ts
│   │   ├── CreateProduct.ts
│   │   └── GetUsers.ts
│   └── ports/
├── infrastructure/
│   ├── api/
│   │   ├── axiosClient.ts
│   │   └── repositories/
│   │       ├── AxiosProductRepository.ts
│   │       └── AxiosUserRepository.ts
│   └── storage/
└── presentation/
    ├── components/
    ├── hooks/
    ├── stores/
    ├── layouts/
    └── pages/
```

## Ejemplo

El dominio define lo que necesita:

```ts
export interface ProductRepository {
  getAll(): Promise<Product[]>;
  create(product: CreateProductInput): Promise<Product>;
}
```

La infraestructura implementa esa necesidad con Axios:

```ts
export class AxiosProductRepository implements ProductRepository {
  async getAll(): Promise<Product[]> {
    const response = await httpClient.get<ProductDTO[]>("/products");

    return response.data.map(productMapper.toDomain);
  }
}
```

React utiliza el caso de uso:

```ts
const getProducts = new GetProducts(productRepository);

const products = await getProducts.execute();
```

## Ventajas

- La lógica queda desacoplada de las librerías.
- Testing sencillo.
- Puedes cambiar Axios por Fetch.
- Puedes cambiar Zustand por Redux.
- Puedes reutilizar reglas sin React.

## Problemas

Para un CRUD común puede producir demasiadas interfaces, clases, adaptadores y mappers.

Por ejemplo, crear:

```
ProductRepository
AxiosProductRepository
GetProductsUseCase
ProductDTO
ProductMapper
ProductEntity
```

solo para hacer un `GET /products` puede ser más complejidad de la necesaria.

## Cuándo usarla

Cuando el frontend tiene reglas de negocio importantes y no es solamente una interfaz sobre una API.

Ejemplo: cálculos financieros, permisos complejos, flujos de aprobación o configuración dinámica.