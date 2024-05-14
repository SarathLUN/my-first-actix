# My First Actix CRUD API

This is my practice project for learning purpose only.

### Prerequisites: 
- First we start by creating a project with `cargo` command
- Make sure you have command `make` ready in your machine.
- In this project we will use [`Makefile`](./Makefile). Read the file before you execute.
- The [docker service](https://www.docker.com/products/docker-desktop/), make sure you have it running.

### Start

- in the terminal, make sure you are in the root folder of this project.
- you should have the `Makefile` ready in the project root folder.
- now run `make install`, this will add all required Rust dependencies into our project.
- then run `make create_project_structure` this will initialize the Postgres container.
- then run `make create_docker_container` this will initialize the Postgres container.
- then run `make create_postgres_db` this will create a database in side the Postgres container.

### Implement Models

- start with `models/game.rs`
- make sure you declare module as public in `models/mod.rs`

### Implement Routes

- start with `routes/game_routes.rs`
- then `routes/config.rs`
- public all modules in `routes/mod.rs`

### Implement Main

- file `main.rs`
- also make use of the environment variable from file `.env`

### Database migration

- run `make create_migrations` this will create initial database migration files (up & down) inside the [migrations](migrations)
- setup schema in the `init.up` file
- then run `make migrate-up`, at this step we should get the table `games` in our database `soccer_rusty_db`.

### Start the server:

- run `cargo run`

### Client test:

- recommended [Postman](https://www.postman.com/).
- I'm using RustRover which have `HTTP Client` feature, so I create file: [My First Actix Client.http](./My%20First%20Actix%20Client.http)
- first I want to test with health checker

```http request
### Health Checker
GET http://localhost:8080/api/health-checker
Accept: application/json
```

- output:

![Health Checker](/images%2FScreenshot%202024-05-13%20at%2011.12.55%E2%80%AFPM.png)

- here I test with the create game first so that we have record to query back

```http request
### create game
POST http://localhost:8080/api/games/game
Content-Type: application/json

{
  "field_name":"Soccer Planet",
  "address": "444 NW Miami FL 32342",
  "day": "Mon 12-00"
}
```

- output:

![create game](/images%2FScreenshot%202024-05-13%20at%2011.19.16%E2%80%AFPM.png)

- test query all games

```http request
### get all games
GET http://localhost:8080/api/games
Content-Type: application/json
```

- output:

![get all games](/images%2FScreenshot%202024-05-13%20at%2011.21.28%E2%80%AFPM.png)

- test query game by ID

```http request
### get game by ID
GET http://localhost:8080/api/games/game/3a6403a9-527e-439a-a9c9-412e12d3be09
Content-Type: application/json
```

- output:

![get game by ID](/images%2FScreenshot%202024-05-13%20at%2011.24.42%E2%80%AFPM.png)

- test update game by ID

```http request
### update game by ID
PUT http://localhost:8080/api/games/game/3a6403a9-527e-439a-a9c9-412e12d3be09
Content-Type: application/json

{
  "field_name":"Soccer UPDATED",
  "address": "UPDATED ADDRESS"
}
```

- output:

![update game by ID](/images%2FScreenshot%202024-05-13%20at%2011.26.54%E2%80%AFPM.png)

- test delete game by its ID

```http request
### delete game by ID
DELETE http://localhost:8080/api/games/game/3a6403a9-527e-439a-a9c9-412e12d3be09
```

- output:

![delete game by ID](/images%2FScreenshot%202024-05-13%20at%2011.28.42%E2%80%AFPM.png)

