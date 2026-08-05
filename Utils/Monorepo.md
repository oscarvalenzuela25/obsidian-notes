## Turborepo
Turborepo reluce mucho cuando no tienes problemas de compatibilidad con tecnologías, si es asi es preferible que vayas por la opción de abajo que es un tipo de monorepo pero sin una tecnología para gestionar monorepos.
Instalación
```
npx create-turbo@latest
```
Esto va a crear 2 apps y 3 librerías compartidas
- Vamos a tener nuestras apps en la carpeta apps
- Vamos a tener nuestras librerías o cosas a compartir en la carpeta packages
```
Application packages
 - apps\docs
 - apps\web
Library packages
 - packages\eslint-config
 - packages\typescript-config
 - packages\ui
```
Para dejar el proyecto limpio y configurado hay que hacer lo siguiente:
En package.json
```json
{
  "name": "products",
  "private": true,
  "scripts": {
    "build": "turbo run build",
    "dev": "turbo run dev",
    "lint": "turbo run lint",
    "format": "prettier --write \"**/*.{ts,tsx,md}\"",
    "check-types": "turbo run check-types"
  },
  "devDependencies": {
    "prettier": "^3.7.4",
    "turbo": "^2.10.8"
  },
  "engines": {
    "node": ">=18"
  },
  "devEngines": {
    "packageManager": {
      "name": "npm",
      "version": ">=10.x <=11.x",
      "onFail": "warn"
    }
  },
  "workspaces": [
    "apps/*",
    "packages/*"
  ]
}
```
En los scripts, si quieres levantar una app sola, debes tener este script
```json
"dev:client": "turbo dev --filter=client",
```
- Ahora dejamos app/ limpia
- Ahora dejamos packages/ limpio
El .gitignore queda asi
```
# See https://help.github.com/articles/ignoring-files/ for more about ignoring files.


# Dependencies
node_modules


# Local env files
.env
.env.local
.env.development.local
.env.test.local
.env.production.local
  

# Testing
coverage


# Turbo
.turbo


# Build Outputs
build
dist


# Debug
npm-debug.log*

# Misc
.DS_Store
*.pem
```
y el turbo.json queda asi
```json
{
  "$schema": "https://turborepo.dev/schema.json",
  "ui": "tui",
  "tasks": {
    "build": {
      "dependsOn": ["^build"]
    },
    "lint": {
      "dependsOn": ["^lint"]
    },
    "check-types": {
      "dependsOn": ["^check-types"]
    },
    "dev": {
      "cache": false,
      "persistent": true
    }
  }
}
```

## Monorepo sin tecnologias para monorepo
Este monorepo busca que cada una de las apps queden aisladas y el package.json que tiene en la raiz del proyecto es para levantarlos pero cada una vive en su espacio.
quedaria algo asi
```
Monorepo/
├── apps/
│   ├── blog-client/
│   │   ├── package.json
│   │   ├── package-lock.json
│   │   └── node_modules/
│   └── blog-cms/
│       ├── package.json
│       ├── package-lock.json
│       └── node_modules/
└── package.json
```
y el package.json quedaría algo asi
```json
{
  "name": "products",
  "private": true,
  "scripts": {
    "dev:blog-client": "npm --prefix apps/blog-client run dev",
    "dev:blog-cms": "npm --prefix apps/blog-cms run dev",
    "build": "npm run build:blog-client && npm run build:blog-cms",
    "build:blog-client": "npm --prefix apps/blog-client run build",
    "build:blog-cms": "npm --prefix apps/blog-cms run build",
    "install:blog-client": "npm --prefix apps/blog-client install",
    "install:blog-cms": "npm --prefix apps/blog-cms install",
    "install:all": "npm run install:blog-client && npm run install:blog-cms"
  },
  "engines": {
    "node": ">=22.12.0"
  },
  "devEngines": {
    "packageManager": {
      "name": "npm",
      "version": ">=10.x <=11.x",
      "onFail": "warn"
    }
  }
}
```