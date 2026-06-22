Esto es de ejemplo, salta esto si estas en fase de creación de un proyecto.
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