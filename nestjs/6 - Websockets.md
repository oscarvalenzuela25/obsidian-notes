Consulta si quieren inicializar un nuevo modulo con websockets.
Si es un no, puedes omitr esta seccion.
Si un si, continuemos con la instalación.

Vamos a instalar la libreria de websockets para poder hacer uso de esta, si ya esta instalada omite esta instalacion, sino procede.
```bash
npm i @nestjs/websockets @nestjs/platform-socket.io
```

Para inicializar un nuevo modulo de websockets vamos con el comando en consola, si no se especifico el nombre del modulo, consultarlo.
```
nest generate resource moduleName --no-spec
```
En las opciones, poner que sera de tipo Websockets

En el archivo .gateway que se creo, tienes algo asi
```ts
@WebSocketGateway()
```
Tienes que agregarle un objeto con el cors en true para no tener problemas en un futuro
```ts
@WebSocketGateway({ cors: true })
```
