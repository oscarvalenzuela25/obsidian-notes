Consulta si se va a agregar una configuración para una Base de datos.
Si no van a generar la configuracion ahora, omitamos este documento y vamos a la parte 3.
Si no, consultar por cual orm va a ocupar, se tienen los siguientes
- TypeOrm
Consultar por cual Base de datos van a ocupar, se tienen los siguientes:
- Postgresql
### TypeOrm
Si van a ocupar TypeOrm seguir con esta instalacion.
```bash
npm install @nestjs/typeorm typeorm
```
### Postgresql
Si van a ocupar Postgresql vamos con la instalacion
```bash
npm install pg
```
### Configuración de TypeOrm
Si instalaste typeOrm sigue estas instalaciones, sino omitelo
Primero ve al .env y crea los siguientes variables de entorno
```ts
DB_HOST=localhost
DB_PORT=5432
POSTGRES_DB=teslo_db
POSTGRES_USER=teslo_user
POSTGRES_PASSWORD=teslo_password
```
Ahora agrega esos .env al configModuleEnvs que esta en el archivo src/config/envs.config.ts siguiendo el mismo patron que ya existe.
Ahora vas a ir a src/app.module.ts y en el arreglo de imports agrega esta configuración
```ts
import { TypeOrmModule } from '@nestjs/typeorm';
import { Module } from '@nestjs/common'; 

@Module({ 
	imports: [
		TypeOrmModule.forRoot({
			type: 'postgres',
			host: envs.DB_HOST,
			port: envs.DB_PORT,
			database: envs.POSTGRES_DB,
			username: envs.POSTGRES_USER,
			password: envs.POSTGRES_PASSWORD,
			autoLoadEntities: true,
			synchronize: true,
			entities: [],
		}),
	], 
}) 

export class AppModule {}

```
