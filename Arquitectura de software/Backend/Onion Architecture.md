Onion Architecture organiza el sistema en círculos concéntricos:

```
Infrastructure
  Application
    Domain Services
      Domain Model
```

## FileSystem

Puede verse prácticamente igual que Clean Architecture:

```
src/
└── modules/
    └── jobs/
        ├── domain/
        ├── application/
        ├── infrastructure/
        └── presentation/
```

## Diferencia práctica

|Arquitectura|Énfasis|
|---|---|
|Clean|Capas y casos de uso|
|Hexagonal|Puertos y adaptadores|
|Onion|Dominio en el centro|
|Tu estructura|Mezcla de las tres|

En proyectos reales suelen combinarse. No necesitas escoger dogmáticamente una sola.