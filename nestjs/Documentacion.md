### Swagger
Instalacion de la libreria para nestjs
```bash
npm install --save @nestjs/swagger
```

Vamos al main.ts
```ts
import { NestFactory } from '@nestjs/core';
import { SwaggerModule, DocumentBuilder } from '@nestjs/swagger';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);

  const config = new DocumentBuilder()
    .setTitle('Course API') // Title
    .setDescription('API documentation') // Subtitle
    .setVersion('1.0') // Version
    .build();
  const documentFactory = () => SwaggerModule.createDocument(app, config);
  SwaggerModule.setup('/documentation', app, documentFactory); // initial path

  await app.listen(process.env.PORT ?? 3000);
}
bootstrap();
```

Para agregar nombres custom a las secciones, usamos el @ApiTags("nombre de la seccion")
Vamos a los controladores
```ts
@ApiTags('Authorization')
@Controller('auth')
export class AuthController {
constructor(private readonly authService: AuthService) {}
}
```

Para agregar codigos de responses a las peticiones, usamos el @ApiResponse(options) en los controladores
```ts
@Post()
@Auth(ValidRoles.admin)
@ApiResponse({
status: 201,
description: 'The product has been successfully created.',
type: Product, // entity
})
@ApiResponse({
status: 400,
description: 'The product has not been created.',
})
@ApiResponse({
status: 403,
description:
'Forbidden. You do not have the necessary permissions to create a product.',
})
create(@Body() createProductDto: CreateProductDto, @GetUser() user: User) {
return this.productsService.create(createProductDto, user);
}
```
Si queremos que en el 201 aparezca el response type o el schema del response, tenemos que ir al entity del controlador y poner @ApiProperty(), el ApiProperty tiene varios valores para agregar.
```ts
export class Product {
@ApiProperty({
example: '9ec96150-9783-4380-99c3-01942f80cf8b',
description: 'Product Id',
uniqueItems: true,
})
@PrimaryGeneratedColumn('uuid')
id!: string;

@ApiProperty({
example: 'T-shirt',
description: 'Product title',
})
@Column('text', { unique: true })
title!: string;

@ApiProperty({
example: 500,
description: 'Product price',
default: 0,
})
@Column('float', { default: 0 })
price!: number;

@ApiProperty({
example: 'This is a description',
description: 'Product description',
nullable: true,
})
@Column('text', { nullable: true })
description!: string;

@ApiProperty({
example: 't-shirt',
description: 'Product slur in url',
uniqueItems: true,
})
@Column('text', { unique: true })
slug!: string;

@ApiProperty({
example: 1,
description: 'Product stock',
default: 0,
})
@Column('int', { default: 0 })
stock!: number;

@ApiProperty({
example: ['xs', 'sm', 'md', 'lg', 'xl'],
description: 'Product sizes',
isArray: true,
})
@Column('text', { array: true })
sizes!: string[];

@ApiProperty({
example: 'unisex',
description: 'Product gender',
})
@Column('text')
gender!: string;

@ApiProperty({
example: [],
description: 'Product tags',
isArray: true,
})

@Column('text', { array: true, default: [] })
tags!: string[];
}
```
Esto tambien se puede ocupar para documentar los DTO, asi se tendra automaticamente la documentación de eso.
Cuando tenemos DTO de updates, este toma el DTO del create y le agrega el PartialType que viene de mapper-types, para la documentación swagger tiene ese mismo PartialType de su libreria para poder hacer la documentación de esta.
