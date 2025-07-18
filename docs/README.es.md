# Entrega Proyecto de Backend con Node.js

`>` **Proyectos KeepCoding - Web 18:** 📁 [repos-kc-web-18.md](https://github.com/pablo-sch/pablo-sch/blob/main/docs/repos-kc-web-18.md)

`>` **Selecciona tu Idioma:** [Inglés](README.md) 🔄 [Alemán](README.de.md)

<!-- ------------------------------------------------------------------------------------------- -->

## Objetivo del Proyecto

Con el fin de ejercitar y demostrar los conocimientos adquiridos en clases virtuales, este proyecto consiste en desarrollar una aplicación con SSR (ejs) para un servicio de venta de artículos de segunda mano llamado Nodepop. El servicio mantiene productos a la venta y permite buscar como poner filtros por varios
criterios.

<!-- ------------------------------------------------------------------------------------------- -->

## Conocimientos Aprendidos y Trabajados

- **Node.js**: modelo orientado a eventos, motor V8, gestión de versiones con nvm/nvs y paquetes con NPM/NPX.
- **JavaScript avanzado**: hoisting, ámbito (`var`/`let`/`const`), prototipos y clases, callbacks, asincronía con promesas y `async/await`.
- **Event Loop y EventEmitter** en Node.js para manejo de eventos.
- **Modularización** con CommonJS (`require`/`module.exports`) y ES Modules (`import`/`export`).
- **Arquitectura MVC** con Express y plantillas EJS; uso de Express Generator.
- **Express.js**: rutas REST (`GET`, `POST`, `PUT`, `DELETE`), parámetros (`req.params`, `req.query`, `req.body`), middlewares (cookie-parser, express-validator), manejo de errores y respuestas (`res.json`, `res.render`, etc.).
- **Bases de datos SQL** (MySQL/MariaDB) con `mysql2/promise` y Docker; consultas CRUD básicas.
- **ORMs**: uso y comparativa de Sequelize, TypeORM, Prisma y Mikro-ORM.
- **MongoDB** (driver oficial): operaciones CRUD avanzadas (operadores, geoespaciales, transacciones); **Mongoose** como ODM para definir esquemas, validaciones, métodos, paginación e índices geoespaciales.
- **Autenticación**: Basic HTTP Auth y basada en sesiones/cookies (anatomía de la cookie y almacenamiento de sesión).
- **Seguridad en contraseñas**: uso de bcrypt, scrypt y argon2 (en lugar de PBKDF2).
- **Herramientas de desarrollo**: Docker para entornos reproducibles, nodemon y cross-env para recarga automática y variables de entorno en desarrollo.

<!-- ------------------------------------------------------------------------------------------- -->

## Detalles del Proyecto

### 1. Listado de Posts

- Cada post muestra imagen (o placeholder), nombre, descripción, precio y compra/venta.
- Se obtienen vía `GET /api/v1/adverts` con filtros opcionales: `name=`, `sale=`, `price=`, `tags=`, `skip=`, `limit=`, `sort=`.
- Estados UI: Vacío (sin posts), Carga, Error, Éxito (mostrar lista).
- Cada post es clicable y lleva a `/posts/:id`.
- Si el usuario está logueado (token), aparece botón “Crear Post” → `/posts/new`.

### 2. Detalle de Post

- Muestra imagen (o placeholder), nombre, descripción, precio, compra/venta, tags y propietario.
- Se obtiene vía `GET /api/v1/adverts/:id`. Si no existe, 404.
- Estados UI: Vacío (404), Carga, Error, Éxito (mostrar detalles).
- Si el usuario autenticado es propietario, botón “Eliminar” → `DELETE /api/v1/adverts/:id`, confirmar antes.

### 3. Creación de un Post

- Acceso solo si está logueado; si no, redirige a `/posts` con aviso.
- Formulario con: Foto (opcional), Nombre*, Descripción*, Precio*, Compra/Venta*, Tags\*.
- Al enviar: `POST /api/v1/adverts` (header `Authorization: Bearer <token>`), body en `multipart/form-data` o JSON.
- Estados UI: Carga, Error (validación o servidor), Éxito (redirigir a `/posts/:id`).

### 4. Login

- Formulario con Email*, Contraseña*, (Recordar sesión).
- `POST /api/auth/login`, payload `{ email, password }`.
- Estados UI: Carga, Error (credenciales inválidas), Éxito (guardar token y redirigir a `/posts`).

### 5. Registro

- Similar a login, con Email*, Contraseña*, Confirmar Contraseña\*.
- `POST /api/auth/signup`, payload `{ email, password }`.
- Estados UI: Carga, Error (email registrado o validación), Éxito (guardar token y redirigir o ir a login).

### 6. Objetivos Opcionales

- Paginación en listado: `?limit=10&skip=<offset>`, botones “Anterior”/“Siguiente”.
- Buscador dinámico: input con debounce que consulta `GET /api/v1/adverts?name=`.
- Edición de posts (propietario): formulario prellenado en `/posts/:id/edit`, `PUT /api/v1/adverts/:id`.
- Filtrado por tags estáticas: checkboxes o dropdown con tags (`work`, `lifestyle`, `motor`, `mobile`).
- Tags dinámicos: obtener lista desde `GET /api/v1/adverts/tags` y generar filtro en frontend.

### Consideraciones

- El script `initDB.js` debe incluir ejemplos de usuarios y productos para pruebas.
- Para filtros, construir un objeto `filters` según los parámetros recibidos y pasarlo a `Product.find(filters)` junto con opciones de paginación y ordenación.
- Al enviar arrays (por ejemplo, `tags`), asegurarse de usar JSON en el cuerpo de la petición.

<!-- ------------------------------------------------------------------------------------------- -->

## Tecnologías Utilizadas

- **Lenguajes:** EJS, CSS, JavaScript.
- **Dependencias a destacar (Node.js):** express, eslint, nodemon, mongoose, morgan y multer.

<!-- ------------------------------------------------------------------------------------------- -->

## Instrucciones de Instalación y Uso

### 1. Requisitos de Software

- **[Node.js](https://nodejs.org/en/download/)** (testeado en la versión **v22.15.1**)
- **[Git](https://git-scm.com/downloads)** (testeado en la versión **2.47.1.windows.1**)
- **[Visual Studio Code](https://code.visualstudio.com/)** (testeado en la versión **1.99.0**)
- **[MongoDB](https://www.mongodb.com/try/download/community)** (probado en la versión **8.0.5**)
- **[NoSQLBooster for MongoDB](https://nosqlbooster.com/downloads)** (probado en la versión **9.1.5**)
- **Live Server** (extensión de VS Code, _opcional_)

### 2. Clonación del Repositorio

```bash
git clone https://github.com/pablo-sch/keepcoding-04-node-backend.git
```

`>` **Ver Demo de Clonanción en VSCode:** 🎥 [Gif Demo](https://github.com/pablo-sch/pablo-sch/blob/main/etc/clone-tutorial.gif)

### 3. Comandos

**Nota:** Asegúrate de tener MongoDB en funcionamiento en tu dispositivo local.
Luego, sigue estos pasos:

```sh
# Instala las dependencias del proyecto.
npm install

# Inicializa la base de datos (solo necesario en el primer despliegue).
npm run initDB

# Ejecuta el proyecto en modo desarrollo.
npm run dev
npx nodemon .\bin\www
```

<!-- ------------------------------------------------------------------------------------------- -->

## Recursos del Proyecto

`>` **Vista Previa del Proyecto:** 👀 [Vista Previa](preview.md) TODO

<!-- ------------------------------------------------------------------------------------------- -->

## Contribuciones y Licencias

Proyecto bajo licencia MIT. Uso y distribución libres con atribución. No se aceptan contribuciones externas, pero las sugerencias son bienvenidas.
