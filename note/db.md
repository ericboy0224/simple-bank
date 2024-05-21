# DB

## Design

[dbdiagram.io](https://dbdiagram.io/): A free tool to draw ER diagrams by just writing code

- [DBML(Database markdown language)](https://dbml.dbdiagram.io/home): A DSL for writing defining database schema or mental big picture structure
- Exporting DB languages like Postgres or MySQL
- Exporting diagrams with PDF file

## Migration

[go migrate](https://github.com/golang-migrate/migrate): Database migrations written in Go. Use as CLI or import as library.

- Migrate reads migrations from sources and applies them in correct order to a database.
- Drivers are "dumb", migrate glues everything together and makes sure the logic is bulletproof. (Keeps the drivers lightweight, too.)
- Database drivers don't assume things or try to correct user input. When in doubt, fail.

### Installation

#### Ubuntu

```shell
wget http://github.com/golang-migrate/migrate/releases/latest/download/migrate.linux-amd64.deb
sudo dpkg -i migrate.linux-amd64.deb
```

#### MacOS

```shell
brew install golang-migrate
```

### Setup

```shell
mkdir simplebank
cd simplebank
```

```shell
# In /simplebank directory
mkdir -p db/migration
```

```shell
# In /simplebank directory
migrate create -exl sql -dir db/migration/ -seq init-schema
```

## Environment Setup

### Pull postgres

```shell
docker pull postgres:12-alpine
```

### Start a container:

```shell
docker run --name <container_name> -e <environment_variable> -d <image>:<tag>
```

```shell
docker run --name postgres12 -p 5432:5432 -e POSTGRES_USER=root -e PORTGRES_PASSWORD=secret -d postgres:12-alpine
```

### Run command in container

```shell
docker exec -it <container_name_or_id> <command> [args]
```

```shell
docker exec -it postgres12 psql -U root
```

- psql: access postgres console

### Show logs of a container

```shell
docker logs <container_name_or_id>
```

## Management

[Table Plus](https://tableplus.com/): Modern, native, and friendly GUI tool for relational databases: MySQL, PostgreSQL, SQLite & more

### New connection

### Configuration for simple bank

```shell
name: postgres12
host: 10.10.0.107
user: root
password: secret
database: root
```

- Press "test" and make sure all the fields are green
- Press "connect"

### Create tables

- Paste the code that is generated from the [dbdiagram section](#design)
- Select all code and press CMD+Enter
- Press CMD+R to reload the application

### Delete and update tables

- Select all tables from the left bar
- Right click and click delete and check CASCADE
- CMD + s to execute deletion

## DB CRUD

[sqlc](https://docs.sqlc.dev/en/stable/tutorials/getting-started-postgresql.html): sqlc generates type-safe code from SQL

- You write queries in SQL
- You run sqlc to generate code with type-safe interfaces to those queries
- You write application code that calls the generated code
