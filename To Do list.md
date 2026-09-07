- Actualizar lo de translate con el modelo nuevo
- Cambiar el diseño de la BD para que modulo ahora tenga una tabla pivote con user y los modulos van a ir directos con el usuario
# Blueprint: Endpoint `/api/v1/authorization/context` (NestJS)

## 1. Lo importante a tener en cuenta (Reglas de diseño)

1. **Separación de responsabilidades:**
   - `auth`: Autentica (JWT, login, emisión de tokens).
   - `authorization`: Autoriza (roles, permisos/acciones, módulos accesibles).
   - Este endpoint pertenece 100% al módulo de `authorization`.
2. **Propósito del endpoint:**
   - Servir como *bootstrap* o contexto inicial para el frontend tras autenticarse o recargar página (F5).
   - Provee datos para: renderizar el Sidenav dinámico, ocultar/mostrar vistas (`modules`) y habilitar/deshabilitar botones y acciones (`actions`).
3. **Formato dual de acciones y módulos:**
   - `actions`: Array plano de strings (`['users:create', 'invoices:export']`) para verificación inmediata $O(1)$ en directivas y guards de UI.
   - `modules`: Estructura en árbol jerárquico (`parentId`, `submodules`) ordenados por `order` para iterar directamente en el Sidenav.
4. **Optimización de consultas (Evitar N+1):**
   - El servicio debe resolver la consulta de permisos mediante una única consulta SQL optimizada con `JOIN`s o vistas, agregando los roles, acciones y módulos del usuario.
5. **Seguridad:**
   - Ocultar vistas/botones en el frontend es puramente **UX**. Las rutas del backend deben seguir protegidas con Guards (`PermissionsGuard`, `RolesGuard`).

---

## 2. Estructura de archivos (NestJS File System)

```text
src/
└── authorization/
    ├── controllers/
    │   └── authorization.controller.ts
    ├── services/
    │   └── authorization.service.ts
    ├── dto/
    │   ├── user-authorization-context.dto.ts
    │   └── app-module.dto.ts
    ├── interfaces/
    │   └── active-user.interface.ts
    ├── decorators/
    │   └── current-user.decorator.ts
    ├── guards/
    │   └── jwt-auth.guard.ts           # (O importado desde src/auth/guards)
    └── authorization.module.ts
```

## 3. Tipado y DTOs

### `src/authorization/dto/app-module.dto.ts`

typescript

export class AppModuleDto {

  id: string;

  code: string;               // Ej: 'USERS', 'BILLING'

  name: string;               // Nombre visual: 'Gestión de Usuarios'

  path: string;               // Ruta frontend: '/admin/users'

  icon?: string;              // Identificador de icono: 'user-icon'

  order: number;              // Para ordenar en el sidenav

  parentId?: string | null;   // null si es raíz

  submodules?: AppModuleDto[]; // Submódulos anidados

  actions?: string[];         // Acciones específicas de este módulo (opcional)

}

### `src/authorization/dto/user-authorization-context.dto.ts`

typescript

import { AppModuleDto } from './app-module.dto';

export class UserAuthorizationContextDto {

  userId: string;

  roles: string[];            // Ej: ['ADMIN', 'OPERATOR']

  actions: string[];          // Ej: ['users:create', 'users:delete', 'reports:export']

  modules: AppModuleDto[];    // Árbol de navegación para el Sidenav

}

### `src/authorization/interfaces/active-user.interface.ts`

typescript

export interface ActiveUser {

  id: string;

  email: string;

  roles?: string[];

}

### `src/authorization/decorators/current-user.decorator.ts`

typescript

import { createParamDecorator, ExecutionContext } from '@nestjs/common';

import { ActiveUser } from '../interfaces/active-user.interface';

export const CurrentUser = createParamDecorator(

  (data: keyof ActiveUser | undefined, ctx: ExecutionContext) => {

    const request = ctx.switchToHttp().getRequest();

    const user = request.user;

    return data ? user?.[data] : user;

  },

);

---

## 4. Controller

> **Nota sobre el prefijo:** Si en `main.ts` ya tienes `app.setGlobalPrefix('api/v1')`, el decorador se deja como `@Controller('authorization')`. Si no tienes prefijo global, usa `@Controller('api/v1/authorization')`.

### `src/authorization/controllers/authorization.controller.ts`

typescript

import { Controller, Get, UseGuards } from '@nestjs/common';

import { AuthorizationService } from '../services/authorization.service';

import { UserAuthorizationContextDto } from '../dto/user-authorization-context.dto';

import { CurrentUser } from '../decorators/current-user.decorator';

import { ActiveUser } from '../interfaces/active-user.interface';

// Ajusta la ruta de tu JwtAuthGuard según tu proyecto

import { JwtAuthGuard } from '../../auth/guards/jwt-auth.guard';

@Controller('api/v1/authorization')

@UseGuards(JwtAuthGuard)

export class AuthorizationController {

  constructor(private readonly authorizationService: AuthorizationService) {}

  /**

   * Endpoint: GET /api/v1/authorization/context

   * Retorna roles, acciones y árbol de módulos asignados al usuario autenticado.

   */

  @Get('context')

  async getAuthorizationContext(

    @CurrentUser() user: ActiveUser,

  ): Promise<UserAuthorizationContextDto> {

    return this.authorizationService.getUserContext(user.id);

  }

}

---

## 5. Service

### `src/authorization/services/authorization.service.ts`

typescript

import { Injectable } from '@nestjs/common';

import { UserAuthorizationContextDto } from '../dto/user-authorization-context.dto';

import { AppModuleDto } from '../dto/app-module.dto';

@Injectable()

export class AuthorizationService {

  // Inyectar aquí el repositorio o cliente ORM (PrismaService, TypeORM Repository, etc.)

  constructor() {}

  async getUserContext(userId: string): Promise<UserAuthorizationContextDto> {

    // 1. Obtener los roles del usuario

    const roles: string[] = await this.fetchUserRoles(userId);

    // 2. Obtener las acciones (permisos) activas del usuario (por sus roles o asignación directa)

    const actions: string[] = await this.fetchUserActions(userId);

    // 3. Obtener los módulos asignados y estructurarlos en árbol

    const rawModules = await this.fetchUserModules(userId);

    const modules: AppModuleDto[] = this.buildModuleTree(rawModules);

    return {

      userId,

      roles,

      actions,

      modules,

    };

  }

  private async fetchUserRoles(userId: string): Promise<string[]> {

    // TODO: Consulta a BD

    return ['ADMIN'];

  }

  private async fetchUserActions(userId: string): Promise<string[]> {

    // TODO: Consulta a BD (aplanar permisos únicos)

    return ['users:create', 'users:read', 'users:update', 'invoices:read'];

  }

  private async fetchUserModules(userId: string): Promise<AppModuleDto[]> {

    // TODO: Consulta a BD de módulos permitidos

    return [];

  }

  /**

   * Transforma una lista plana de módulos con parentId en un árbol jerárquico

   */

  private buildModuleTree(modules: AppModuleDto[]): AppModuleDto[] {

    const moduleMap = new Map<string, AppModuleDto>();

    const tree: AppModuleDto[] = [];

    modules.forEach((mod) => {

      moduleMap.set(mod.id, { ...mod, submodules: [] });

    });

    moduleMap.forEach((mod) => {

      if (mod.parentId && moduleMap.has(mod.parentId)) {

        moduleMap.get(mod.parentId)!.submodules!.push(mod);

      } else {

        tree.push(mod);

      }

    });

    // Ordenar por la propiedad 'order'

    tree.sort((a, b) => a.order - b.order);

    tree.forEach((parent) => parent.submodules?.sort((a, b) => a.order - b.order));

    return tree;

  }

}

---

## 6. Módulo

### `src/authorization/authorization.module.ts`

typescript

import { Module } from '@nestjs/common';

import { AuthorizationController } from './controllers/authorization.controller';

import { AuthorizationService } from './services/authorization.service';

@Module({

  imports: [

    // Importar aquí módulos de base de datos (PrismaModule, TypeOrmModule.forFeature([...]), etc.)

  ],

  controllers: [AuthorizationController],

  providers: [AuthorizationService],

  exports: [AuthorizationService], // Exportado por si otros módulos necesitan validar permisos

})

export class AuthorizationModule {}

