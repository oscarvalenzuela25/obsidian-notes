Aquí vamos a comenzar con la instalación de un proyecto desde 0 de nestjs, te vas a encontrar con las siguientes situaciones:
Hay secciones que tienes que consultar al usuario antes de continuar.
Hay secciones de ejemplo, omítelas para la instalación, son apuntes o cosas que pueden ayudar cuando necesites contexto de lo que se quiere hacer.
Hay secciones automáticas que tienes que instalarlas sin consultar al usuario.
## Instalar Nestjs CLI
Verifica si esta instalado nestjs CLI, si no instalar con el siguiente comando
```bash
  npm i -g @nestjs/cli
```
## Nuevo proyecto
Para crear un nuevo proyecto, digitar el siguiente comando, consulta por el nombre del proyecto.
```bash
  nest new project-name
```
## Librerías bases a instalar
### Validadores
Librería para validar DTOs
```bash
  npm i class-validator class-transformer
```
### .envs
Librería para utilizar .envs
```bash
  npm i @nestjs/config
```
Después de instalar esta libreria, procede a crear un .env en la raiz del proyecto con el valor base PORT=3000 y busca en el proyecto si existe src/config/envs.config.ts, sino créalo y pon esta configuración base
``` ts
export const configModuleEnvs = () => ({
	PORT: process.env.PORT ? parseInt(process.env.PORT) : 3000,
});
export const envs = configModuleEnvs();
```
### Variables de entorno
src/app.module.ts agregar esta configuración para usar los .env de otra forma
``` ts
import { Module } from '@nestjs/common'; 
import { ConfigModule } from '@nestjs/config'; 

@Module({ 
	imports: [ConfigModule.forRoot()], 
}) 

export class AppModule {}
```
Uso de variables .env en el archivo que se utilizara, esto es de ejemplo.
```ts
constructor( 
	private readonly configService:ConfigService 
){}
```
## Configuraciones Iniciales
Ahora vamos a ir al archivo src/main.ts y empezaremos con la configuración base
Este es un ejemplo del archivo src/main.ts que debe de existir, sino agregar lo que falte.
```ts
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';
import { envs } from './config/envs.config';

async function bootstrap() {
	const app = await NestFactory.create(AppModule);
	await app.listen(envs.PORT);
}
bootstrap();
```

### Base path
Consulta si quieren que el path de los endpoints tengan un prefijo por ejemplo "/api".
Si dicen que no quieren, pasamos a lo siguiente, sino agrega la respuesta al app.setGlobalPrefix abajo del app en la función bootstrap con el prefijo que se quiere.
```ts
 app.setGlobalPrefix('/api');
```

### Global pipes
En el archivo src/main.ts, en la función bootstrap, después del app, este va si o si, no es necesario consultarlo
```ts
import { ValidationPipe } from '@nestjs/common';
  
app.useGlobalPipes(
	new ValidationPipe({
		whitelist: true,
		forbidNonWhitelisted: true,
	}),
);
```
 
### Generar componentes de NestJs
Esto es a modo de ejemplo.
El --no-spec es para que no se creen archivos de .test, consulta siempre si no ponen el --no-spec si es que quieren o no archivos de test para incluir o no este comando.
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
Con esto podemos pasar a el punto [[2 - BD]]