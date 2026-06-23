Esta seccion es de ejemplo, tenlo como contexto para desarrollos futuros, puedes ir a la seccion [[4 - Documentacion]]
```ts
@IsString()
@MinLength(6)
@MaxLength(50)
@Matches(/(?:(?=.*\d)|(?=.*\W+))(?![.\n])(?=.*[A-Z])(?=.*[a-z]).*$/, {
message:
'The password must have a Uppercase, lowercase letter and a number',
})
password!: string;
```
Lo de arriba es igual al siguiente decorador
```ts
 @IsStrongPassword({
        minLength: 6,
        minLowercase: 1,
        minUppercase: 1,
        minNumbers: 1,
        minSymbols: 0,
    })
password!: string;
```