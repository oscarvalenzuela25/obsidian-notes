Consulta si se va a agregar una configuración para una Base de datos.
Si no van a generar la configuración ahora, omitamos este documento y vamos a [[3 - Class Validator]].
Consulta si va a utilizar algun ORM, si la respuesta es no, pasamoa a [[3 - Class Validator]], si la respuesta es si, tenemos las siguientes opciones.
- TypeOrm
Consultar por cual Base de datos van a ocupar, se tienen los siguientes:
- Postgresql
### TypeOrm
Si van a ocupar TypeOrm seguir con esta instalación.
```bash
npm install @nestjs/typeorm typeorm
```
### PostgreSQL
Si van a ocupar PostgreSQL vamos con la instalación
```bash
npm install pg
```
### Configuración de TypeOrm
Si instalaste typeOrm sigue estas instalaciones, sino omítelo
Primero ve al .env y crea los siguientes variables de entorno
```ts
DB_HOST=localhost
DB_PORT=5432
POSTGRES_DB=my_db
POSTGRES_USER=my_user
POSTGRES_PASSWORD=my_password
```
Ahora agrega esos .env al configModuleEnvs que esta en el archivo src/config/envs.config.ts siguiendo el mismo patrón que ya existe.
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
Ahora puedes ir a la sección [[3 - Class Validator]]