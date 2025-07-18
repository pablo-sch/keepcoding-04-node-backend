# Backend Project Submission with Node.js

`>` **KeepCoding Projects - Web 18:** 📁 [repos-kc-web-18.md](https://github.com/pablo-sch/pablo-sch/blob/main/docs/repos-kc-web-18.md)

`>` **Select your Language:** [Spanish](README.es.md) 🔄 [German](README.de.md)

<!-- ------------------------------------------------------------------------------------------- -->

## Project Objective

In order to practice and demonstrate the knowledge acquired in virtual classes, this project consists of developing an SSR (EJS) application for a second-hand items marketplace called Nodepop. The service maintains products for sale and allows searching with filters by various criteria.

<!-- ------------------------------------------------------------------------------------------- -->

## Knowledge Learned and Applied

- **Node.js**: event-driven model, V8 engine, version management with nvm/nvs, and package management with NPM/NPX.
- **Advanced JavaScript**: hoisting, scope (`var`/`let`/`const`), prototypes and classes, callbacks, asynchronicity with promises and `async/await`.
- **Event Loop and EventEmitter** in Node.js for event handling.
- **Modularization** with CommonJS (`require`/`module.exports`) and ES Modules (`import`/`export`).
- **MVC Architecture** with Express and EJS templates; usage of Express Generator.
- **Express.js**: REST routes (`GET`, `POST`, `PUT`, `DELETE`), parameters (`req.params`, `req.query`, `req.body`), middlewares (cookie-parser, express-validator), error handling and responses (`res.json`, `res.render`, etc.).
- **SQL Databases** (MySQL/MariaDB) with `mysql2/promise` and Docker; basic CRUD queries.
- **ORMs**: usage and comparison of Sequelize, TypeORM, Prisma, and Mikro-ORM.
- **MongoDB** (official driver): advanced CRUD operations (operators, geospatial queries, transactions); **Mongoose** as an ODM to define schemas, validations, methods, pagination, and geospatial indexes.
- **Authentication**: Basic HTTP Auth and session/cookie-based authentication (cookie anatomy and session storage).
- **Password Security**: using bcrypt, scrypt, and argon2 (instead of PBKDF2).
- **Development Tools**: Docker for reproducible environments, nodemon and cross-env for automatic reload and environment variables in development.

<!-- ------------------------------------------------------------------------------------------- -->

## Project Details

### 1. Post Listing

- Each post shows an image (or placeholder), name, description, price, and buy/sell indicator.
- Retrieved via  
  `GET /api/v1/adverts`  
  with optional filters: `name=`, `sale=`, `price=`, `tags=`, `skip=`, `limit=`, `sort=`.
- UI states: Empty (no posts), Loading, Error, Success (display list).
- Each post is clickable and leads to `/posts/:id`.
- If the user is logged in (token present), a “Create Post” button appears → `/posts/new`.

### 2. Post Detail

- Displays an image (or placeholder), name, description, price, buy/sell status, tags, and owner.
- Retrieved via  
  `GET /api/v1/adverts/:id`  
  Returns 404 if not found.
- UI states: Empty (404), Loading, Error, Success (display details).
- If the authenticated user is the owner, a “Delete” button appears →  
  `DELETE /api/v1/adverts/:id`  
  with confirmation.

### 3. Create a Post

- Accessible only if logged in; otherwise redirects to `/posts` with a notice.
- Form fields: Photo (optional), Name*, Description*, Price*, Buy/Sell*, Tags\*.
- On submit:  
  `POST /api/v1/adverts`  
  (header `Authorization: Bearer <token>`), body as `multipart/form-data` or JSON.
- UI states: Loading, Error (validation or server), Success (redirect to `/posts/:id`).

### 4. Login

- Form fields: Email*, Password*, (Remember session).
- `POST /api/auth/login`  
  payload `{ "email": "user@example.com", "password": "********" }`.
- UI states: Loading, Error (invalid credentials), Success (save token and redirect to `/posts`).

### 5. Signup

- Similar to login, with Email*, Password*, Confirm Password\*.
- `POST /api/auth/signup`  
  payload `{ "email": "new@example.com", "password": "********" }`.
- UI states: Loading, Error (email taken or validation), Success (save token and redirect or go to login).

### 6. Optional Objectives

- Pagination in listing: `?limit=10&skip=<offset>`, “Previous”/“Next” buttons.
- Dynamic search: input with debounce querying  
  `GET /api/v1/adverts?name=`.
- Post editing (owner only): prefilled form at `/posts/:id/edit`,  
  `PUT /api/v1/adverts/:id`.
- Filtering by static tags: checkboxes or dropdown with tags (`work`, `lifestyle`, `motor`, `mobile`).
- Dynamic tags: get list from  
  `GET /api/v1/adverts/tags`  
  and build frontend filter.

### Considerations

- The `initDB.js` script must include sample users and products for testing.
- For filters, build a `filters` object based on received parameters and pass it to  
  `Product.find(filters)`  
  along with pagination and sorting options.
- When sending arrays (for example, `tags`), ensure to use JSON in the request body.

<!-- ------------------------------------------------------------------------------------------- -->

## Technologies Used

- **Languages:** EJS, CSS, JavaScript.
- **Notable Dependencies (Node.js):** express, eslint, nodemon, mongoose, morgan, and multer.

<!-- ------------------------------------------------------------------------------------------- -->

## Installation and Usage Instructions

### 1. Software Requirements

- **[Node.js](https://nodejs.org/en/download/)** (tested on version **v22.15.1**)
- **[Git](https://git-scm.com/downloads)** (tested on version **2.47.1.windows.1**)
- **[Visual Studio Code](https://code.visualstudio.com/)** (tested on version **1.99.0**)
- **[MongoDB](https://www.mongodb.com/try/download/community)** (tested on version **8.0.5**)
- **[NoSQLBooster for MongoDB](https://nosqlbooster.com/downloads)** (tested on version **9.1.5**)
- **Live Server** (VS Code extension, _optional_)

### 2. Repository Cloning

```bash
git clone https://github.com/pablo-sch/keepcoding-04-node-backend.git
```

`>` **View Cloning Demo in VSCode:** 🎥 [Gif Demo](https://github.com/pablo-sch/pablo-sch/blob/main/etc/clone-tutorial.gif)

### 3. Commands

**Note:** Make sure MongoDB is running on your local machine.  
Then, follow these steps:

```sh
# Install project dependencies.
npm install

# Initialize the database (only required on first deployment).
npm run initDB

# Run the project in development mode.
npm run dev
npx nodemon .\bin\www
```

<!-- ------------------------------------------------------------------------------------------- -->

## Project Resources

`>` **Project Preview:** 👀 [Preview](preview.md)

<!-- ------------------------------------------------------------------------------------------- -->

## Contributions and Licensing

Project licensed under the MIT License. Free to use and distribute with attribution. External contributions are not accepted, but suggestions are welcome.
