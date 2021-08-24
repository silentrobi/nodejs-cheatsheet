# TypeOrm-Js

**Sample project link**: https://github.com/typeorm/javascript-example

# Understanding `ormconfig.js`

Multiple connections are specified in array as mentioned bellow. TypeORM automatically detects `ormconfig.js` in run-time.

```js
module.exports = [
  {
    name: "default",
    type: "postgres", //db type
    host: "localhost", //db host name
    port: "5432", //db port
    username: "root", //db username
    password: "12345", //db password
    database: "demo", //db name
    synchronize: false,
    schema: "dev", //schema name for postgres sql
    logging: false,
    ssl: true, //enable/disable ssl connection
    extra: {
      ssl: {
        rejectUnauthorized: false,
      },
    },
    entities: ["src/entity/Entities.js"], // relative paths for entities (Modifiable)
    migrations: ["src/migration/**/*.js"], // specify relative path of migrations folder  (Modifiable)
    subscribers: ["src/subscriber/**/*.js"], // specify relative path of migrations folder  (Modifiable)
    cli: {
      //cli entry points for different operations
      entitiesDir: "src/entity",
      migrationsDir: "src/migration", //specify migration dir for typeorm cli
      subscribersDir: "src/subscriber",
    },
  },
  {
    name: "seed",
    type: "postgres",
    host: "localhost",
    port: "5432",
    username: "root", //db username
    password: "12345", //db password
    database: "demo", //db name
    synchronize: false,
    schema: "dev", //schema name for postgres sql
    logging: false, // enable/disable logging for SQL operations
    ssl: true, //enable/disable ssl connection
    extra: {
      ssl: {
        rejectUnauthorized: false,
      },
    },
    migrations: ["src/seed/**/*.js"], //specify migration folder
    cli: {
      //cli entry points for different operations
      migrationsDir: "src/seed", //specify migration dir for typeorm cli
    },
  },
];
```

# Migration and Seed Scripts in `package.json`:

```js
"migrate:create": "typeorm migration:create -n",
"migrate:up": "typeorm migration:run",
"migrate:down": "typeorm migration:revert",
"migration:generate": "typeorm migration:generate --o -n",
"seed:generate": "typeorm migration:create -c seed --o -n",
"seed:run": "typeorm migration:run -c seed",
"seed:revert": "typeorm migration:revert -c seed",
```

**Note:** For PostgresSQL Database, schema should be created before running `migration:up`
You can run custom script before migrating

```js
const { createConnection } = require("typeorm");

const schemaName = "dev";
// create typeorm connection
createConnection("default")
  .then((connection) => {
    const entityManager = connection.createEntityManager();
    entityManager.query(
      `CREATE SCHEMA IF NOT EXISTS ${schemaName};`
    );
  })
  .catch((err) => {
    logger.error(err);
    process.exit(1);
  });
```
