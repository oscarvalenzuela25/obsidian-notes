Consulta si se va a agregar la configuración de Auth en esta parte.
Si no, omite esta parte y vamos con el siguiente.
Si va a agregar la configuración, continuemos con las instrucciones.

Consulta si ya tiene un modulo en el cual trabajar.
Si no lo tiene, toca crear uno, preguntar el nombre del nuevo modulo y usa el comando
```
nest generate resource module_name --no-spec
```
Si ya lo tiene omitir el comando de creación.

Toca instalar la dependencia si es que no se tiene
```bash
npm install @nestjs/passport passport
```
Supongamos que tenemos el modulo Auth
### JWT
La configuración para jwt es la siguiente
Vamos a src/auth/auth.module.ts y debemos de tener algo asi.
```ts
import { Module } from '@nestjs/common';
import { AuthService } from './auth.service';
import { AuthController } from './auth.controller';
import { TypeOrmModule } from '@nestjs/typeorm';
import { User } from './entities/user.entity';
import { PassportModule } from '@nestjs/passport';
import { envs } from 'src/config/envs.config';
import { JwtModule } from '@nestjs/jwt';
import { JwtStrategy } from './strategies/jwt.strategy';

  
@Module({
	controllers: [AuthController],
	providers: [AuthService, JwtStrategy],
		imports: [
		TypeOrmModule.forFeature([User]),
		PassportModule.register({ defaultStrategy: 'jwt' }),
		JwtModule.registerAsync({
			imports: [],
			inject: [],
			useFactory: () => ({
				secret: envs.JWT_SECRET,
				signOptions: { expiresIn: '7d' },
			}),
		}),
			// Forma convencional de configurar el JwtModule, pero no permite usar variables de entorno
		// JwtModule.register({
		// secret: envs.JWT_SECRET,
		// signOptions: { expiresIn: '7d' },
		// }),
	],
	exports: [TypeOrmModule, JwtStrategy, PassportModule, JwtModule],
})

export class AuthModule {}
```
El JwtStrategy es una forma para hacer la validación del JWT y este sirve para agregar al Request lo que se necesite y en el caso de devolver false, este arroja un error
Ejemplo
```ts
import { PassportStrategy } from '@nestjs/passport';
import { ExtractJwt, Strategy } from 'passport-jwt';
import { User } from '../entities/user.entity';
import { JwtPayload } from '../interfaces/jwtPayload.interface';
import { InjectRepository } from '@nestjs/typeorm';
import { Repository } from 'typeorm';
import { envs } from 'src/config/envs.config';
import { Injectable, UnauthorizedException } from '@nestjs/common';
  
@Injectable()
export class JwtStrategy extends PassportStrategy(Strategy) {
	constructor(
		@InjectRepository(User)
		private readonly userRepository: Repository<User>,
	) {
	super({
		jwtFromRequest: ExtractJwt.fromAuthHeaderAsBearerToken(),
		secretOrKey: envs.JWT_SECRET,
	});
	}

	async validate(payload: JwtPayload): Promise<User> {
		const { id } = payload;
		const user = await this.userRepository.findOne({ where: { id } });
		if (!user) throw new UnauthorizedException('Invalid token');
		if (!user.isActive) throw new UnauthorizedException('User is not active');
		// Lo que se retorna aquí se asigna a req.user en los controladores que usen esta estrategia
		// Para utilizar el req.user, tienes que utilizar el @UseGuards(AuthGuard('jwt')), con esto usa esta estrategia y asigna el user al request de tipo Request
		
		return user;
	}
}
```
Con esa configuracion con passport podemos validar dentro de los controlador con este decorador
```ts
@UseGuards(AuthGuard('jwt'))
```
