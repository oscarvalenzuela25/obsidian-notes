La arquitectura hexagonal es parecida a Clean Architecture. Su idea central son los **puertos y adaptadores**.

```
src/
├── core/
│   ├── domain/
│   ├── use-cases/
│   └── ports/
├── adapters/
│   ├── inbound/
│   │   ├── react/
│   │   └── zustand/
│   └── outbound/
│       ├── axios/
│       ├── local-storage/
│       └── analytics/
└── app/
```

## Ejemplo

El caso de uso necesita guardar configuración:

```ts
export interface SettingsStorage {
  get(): Settings;
  save(settings: Settings): void;
}
```

Podrías tener distintos adaptadores:

```ts
LocalStorageSettingsAdapter
SessionStorageSettingsAdapter
MemorySettingsAdapter
```

La lógica no sabe cuál utiliza la aplicación.

## Diferencia práctica con Clean Architecture

Ambas tienen objetivos muy similares:

- Clean Architecture enfatiza sus capas.
- Hexagonal enfatiza los puertos y adaptadores.

En un frontend React suelen terminar produciendo estructuras parecidas.

## Cuándo usarla

Cuando la aplicación se conecta con múltiples servicios:

- API REST.
- WebSocket.
- LocalStorage.
- IndexedDB.
- Analytics.
- Feature flags.
- Distintos backends según el cliente.