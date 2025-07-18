# Backend-Projektabgabe mit Node.js

`>` **KeepCoding Projekte - Web 18:** 📁 [repos-kc-web-18.md](https://github.com/pablo-sch/pablo-sch/blob/main/docs/repos-kc-web-18.md)

`>` **Wähle deine Sprache:** [Englisch](README.md) 🔄 [Spanish](README.es.md)

<!-- ------------------------------------------------------------------------------------------- -->

## Projektziel

Um die in den virtuellen Kursen erworbenen Kenntnisse zu üben und zu demonstrieren, besteht dieses Projekt darin, eine SSR-(EJS)-Anwendung für einen Second-Hand-Marktplatz namens Nodepop zu entwickeln. Der Service verwaltet Verkaufsartikel und ermöglicht die Suche mit Filtern nach verschiedenen Kriterien.

<!-- ------------------------------------------------------------------------------------------- -->

## Gelernte und Angewendete Kenntnisse

- **Node.js**: ereignisgesteuertes Modell, V8-Engine, Versionsverwaltung mit nvm/nvs und Paketverwaltung mit NPM/NPX.
- **Fortgeschrittenes JavaScript**: Hoisting, Scope (`var`/`let`/`const`), Prototypen und Klassen, Callbacks, Asynchronität mit Promises und `async/await`.
- **Event Loop und EventEmitter** in Node.js zur Ereignisverwaltung.
- **Modularisierung** mit CommonJS (`require`/`module.exports`) und ES Modules (`import`/`export`).
- **MVC-Architektur** mit Express und EJS-Templates; Nutzung des Express Generators.
- **Express.js**: REST-Routen (`GET`, `POST`, `PUT`, `DELETE`), Parameter (`req.params`, `req.query`, `req.body`), Middlewares (cookie-parser, express-validator), Fehlerbehandlung und Antworten (`res.json`, `res.render` usw.).
- **SQL-Datenbanken** (MySQL/MariaDB) mit `mysql2/promise` und Docker; grundlegende CRUD-Abfragen.
- **ORMs**: Nutzung und Vergleich von Sequelize, TypeORM, Prisma und Mikro-ORM.
- **MongoDB** (offizieller Treiber): erweiterte CRUD-Operationen (Operatoren, Geo-Abfragen, Transaktionen); **Mongoose** als ODM zur Definition von Schemas, Validierungen, Methoden, Paginierung und Geo-Indizes.
- **Authentifizierung**: Basic HTTP Auth und Session-/Cookie-basierte Authentifizierung (Cookie-Aufbau und Session-Speicherung).
- **Passwortsicherheit**: Einsatz von bcrypt, scrypt und argon2 (anstelle von PBKDF2).
- **Entwicklungstools**: Docker für reproduzierbare Umgebungen, nodemon und cross-env für automatisches Neuladen und Umgebungsvariablen im Development.

<!-- ------------------------------------------------------------------------------------------- -->

## Projektdetails

### 1. Auflisten von Posts

- Jeder Post zeigt ein Bild (oder Platzhalter), Name, Beschreibung, Preis und Kauf/Verkauf-Indikator.
- Abfrage über  
  `GET /api/v1/adverts`  
  mit optionalen Filtern: `name=`, `sale=`, `price=`, `tags=`, `skip=`, `limit=`, `sort=`.
- UI-Zustände: Leer (keine Posts), Laden, Fehler, Erfolg (Liste anzeigen).
- Jeder Post ist anklickbar und führt zu `/posts/:id`.
- Wenn der Benutzer eingeloggt ist (Token vorhanden), erscheint ein Button „Post erstellen“ → `/posts/new`.

### 2. Post-Detail

- Zeigt Bild (oder Platzhalter), Name, Beschreibung, Preis, Kauf/Verkauf-Status, Tags und Eigentümer.
- Abfrage über  
  `GET /api/v1/adverts/:id`  
  Gibt 404 zurück, wenn nicht gefunden.
- UI-Zustände: Leer (404), Laden, Fehler, Erfolg (Details anzeigen).
- Wenn der authentifizierte Benutzer Eigentümer ist, erscheint ein Button „Löschen“ →  
  `DELETE /api/v1/adverts/:id`  
  mit Bestätigung.

### 3. Erstellen eines Posts

- Nur zugänglich, wenn eingeloggt; sonst Weiterleitung zu `/posts` mit Hinweis.
- Formularfelder: Foto (optional), Name*, Beschreibung*, Preis*, Kauf/Verkauf*, Tags\*.
- Beim Absenden:  
  `POST /api/v1/adverts`  
  (Header `Authorization: Bearer <token>`), Body als `multipart/form-data` oder JSON.
- UI-Zustände: Laden, Fehler (Validierung oder Server), Erfolg (Weiterleitung zu `/posts/:id`).

### 4. Login

- Formularfelder: E-Mail*, Passwort*, (Sitzung merken).
- `POST /api/auth/login`  
  Payload `{ "email": "user@example.com", "password": "********" }`.
- UI-Zustände: Laden, Fehler (ungültige Anmeldedaten), Erfolg (Token speichern und Weiterleitung zu `/posts`).

### 5. Registrierung

- Ähnlich wie Login, mit E-Mail*, Passwort*, Passwort bestätigen\*.
- `POST /api/auth/signup`  
  Payload `{ "email": "new@example.com", "password": "********" }`.
- UI-Zustände: Laden, Fehler (E-Mail bereits vergeben oder Validierung), Erfolg (Token speichern und Weiterleitung oder zur Login-Seite).

### 6. Optionale Ziele

- Paginierung in der Auflistung: `?limit=10&skip=<offset>`, Buttons „Vorherige“/„Nächste“.
- Dynamische Suche: Eingabefeld mit Debounce, das `GET /api/v1/adverts?name=` abfragt.
- Post-Bearbeitung (nur Eigentümer): vorbefülltes Formular unter `/posts/:id/edit`,  
  `PUT /api/v1/adverts/:id`.
- Filtern nach statischen Tags: Checkboxes oder Dropdown mit Tags (`work`, `lifestyle`, `motor`, `mobile`).
- Dynamische Tags: Liste abrufen über  
  `GET /api/v1/adverts/tags`  
  und Filter im Frontend generieren.

### Überlegungen

- Das Skript `initDB.js` muss Beispielbenutzer und -produkte für Tests beinhalten.
- Für Filter ein `filters`-Objekt basierend auf empfangenen Parametern erstellen und an  
  `Product.find(filters)`  
  zusammen mit Paginierungs- und Sortieroptionen übergeben.
- Beim Senden von Arrays (z. B. `tags`) JSON im Request-Body verwenden.

<!-- ------------------------------------------------------------------------------------------- -->

## Verwendete Technologien

- **Sprachen:** EJS, CSS, JavaScript.
- **Bemerkenswerte Abhängigkeiten (Node.js):** express, eslint, nodemon, mongoose, morgan und multer.

<!-- ------------------------------------------------------------------------------------------- -->

## Installations- und Nutzungshinweise

### 1. Softwareanforderungen

- **[Node.js](https://nodejs.org/en/download/)** (getestet mit Version **v22.15.1**)
- **[Git](https://git-scm.com/downloads)** (getestet mit Version **2.47.1.windows.1**)
- **[Visual Studio Code](https://code.visualstudio.com/)** (getestet mit Version **1.99.0**)
- **[MongoDB](https://www.mongodb.com/try/download/community)** (getestet mit Version **8.0.5**)
- **[NoSQLBooster for MongoDB](https://nosqlbooster.com/downloads)** (getestet mit Version **9.1.5**)
- **Live Server** (VS Code-Erweiterung, _optional_)

### 2. Repository-Klonen

```bash
git clone https://github.com/pablo-sch/keepcoding-04-node-backend.git
```

`>` **Klon-Demo in VSCode ansehen:** 🎥 [Gif Demo](https://github.com/pablo-sch/pablo-sch/blob/main/etc/clone-tutorial.gif)

### 3. Befehle

**Hinweis:** Stelle sicher, dass MongoDB auf deinem lokalen Gerät läuft.  
Führe dann folgende Schritte aus:

```sh
# Installiere die Projektabhängigkeiten.
npm install

# Initialisiere die Datenbank (nur beim ersten Deployment erforderlich).
npm run initDB

# Starte das Projekt im Entwicklungsmodus.
npm run dev
npx nodemon .\bin\www
```

<!-- ------------------------------------------------------------------------------------------- -->

## Projektressourcen

`>` **Projektvorschau:** 👀 [Vorschau](preview.md) TODO

<!-- ------------------------------------------------------------------------------------------- -->

## Beiträge und Lizenzierung

Projekt unter MIT-Lizenz. Frei zur Nutzung und Weitergabe mit Namensnennung. Externe Beiträge werden nicht akzeptiert, aber Vorschläge sind willkommen.
