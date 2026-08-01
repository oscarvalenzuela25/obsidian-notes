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