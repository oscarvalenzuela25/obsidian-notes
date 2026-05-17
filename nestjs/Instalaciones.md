## Instalar NestJs CLI
```bash
  npm i -g @nestjs/cli
```
## Nuevo proyecto
```bash
  nest new project-name
```
## Librerías útiles
### Validadores
```bash
  npm i class-validator class-transformer
```
### .envs
```bash
  npm i @nestjs/config
```
### TypeOrm
```bash
npm install --save @nestjs/typeorm typeorm
```
### PostgreSql
```bash
npm install --save @nestjs/typeorm typeorm
```

## Generar componentes de NestJs
- El --no-spec es para que no se creen archivos de .test
```
 # Comando basico
 nest generate <componente> <name> --no-spec
 
 # Crear un recurso completo 
 nest generate resource <name> --no-spec
 
 # Crear una clase 
 nest generate cl <name> --no-spec
 
 # Crear un controlador 
 nest generate co <name> --no-spec
 
 # Crear un decorador 
 nest generate d <name> --no-spec
 
 # Crear un guard 
 nest generate gu <name> --no-spec
 
 # Crear un interceptor 
 nest generate in <name> --no-spec
 
 # Crear un módulo
  nest generate mo <name> --no-spec
 
 # Crear un pipe 
 nest generate pi <name> --no-spec
 
 # Crear un servicio 
 nest generate s <name> --no-spec
 
```
## Configuraciones
### Global pipes
```
app.useGlobalPipes( 
	new ValidationPipe({ 
		whitelist: true, 
		forbidNonWhitelisted: true, 
	})
);
```
### Variables de entorno
* app.module.ts
```
import { Module } from '@nestjs/common'; 
import { ConfigModule } from '@nestjs/config'; 

@Module({ 
	imports: [ConfigModule.forRoot()], 
}) 

export class AppModule {}
```
- Uso de variables .env en el archivo que se utilizara
```
constructor( 
	private readonly configService:ConfigService 
){}
```