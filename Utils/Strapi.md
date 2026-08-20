Cosas que hacer cuando implementas strapi o a tener en cuenta
- Cuando creas algo desde el panel de administración se crea archivos en la carpeta api.
- En la sección de Content type builder es donde creas el esquema de strapi.
- Tenemos los siguientes objetos a utilizar en strapi:
	- Collection types, en resumen son campos que se pueden repetir las entradas, en resumen cuando creas uno, es como crear una tabla para rellenar.
	- Single types, estos son únicos, tomalo como un objeto que puedes actualizar pero solo tiene 1 registro.
	- Components, son componentes reutilizables que vienen en las peticiones de los collection types.
- En la seccion de Content manager es donde creamos las entradas.
- Si queremos cambiar los titulos o placeholder de idioma o lo que sea de los campos que especificamos en algún collection o single types, debemos de ir a Content manager:
	- Si es Collection types, vas a create new entry -> accionable de 3 puntos -> Configure the view -> en Displayed Fields al hacer click en un campo puedes editarlo.
- 
Los roles dentro de strapi funcionan asi
- Administration Panel Roles: Controla lo que empleados y administradores pueden hacer en `/admin`
- Users & Permissions Roles: Controla usuarios de la aplicación que consumen `/api`
- API Tokens: Permiten que aplicaciones o servidores consuman `/api` sin iniciar sesión como usuario
La Api que genera:
Si tenemos un collection types "Tags", estos endpoints estarán disponibles, si es que tienes una api key con permisos.
```
GET    /api/tags
GET    /api/tags/:documentId
POST   /api/tags
PUT    /api/tags/:documentId
DELETE /api/tags/:documentId
```
