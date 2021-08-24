# ExpressJs-Js

## Project setup

`npm init` 

## Understanding `package.json`

It contains project dependencies and scripts to run node application.

```js
{
  "name": "demo", //project name
  "version": "1.0.0", // project version https://docs.npmjs.com/about-semantic-versioning
  "description": "demo application", //project description
  "main": "index.js", //primary entry point of your program.
  "scripts": {
    //custom npm scripts
    "start": "node index.js", // run with [npm run start]
    "start:dev": "nodemon index.js" // run with [npm run start:dev]'
  },

  "author": "Mohammad Abu Musa Rabiul",
  "license": "ISC",
  "dependencies": {
    //Contains production level dependencies. required to build the project
    "@token-org/tokenstore-init-orm-lib": "^1.0.12",
    "bluebird": "^3.7.2",
    "body-parser": "^1.19.0",
    "express": "^4.17.1",
    "pg": "^8.5.1",
    "prettier": "^2.2.0",
    "typeorm": "^0.2.34",
    "typeorm-naming-strategies": "^2.0.0",
  },
  "devDependencies": {
    //Only required during project development
    "babel-eslint": "^10.1.0",
    "prettier-eslint": "^12.0.0",
    "nodemon": "^2.0.6"
  }
}
```
## Useful commands

- Install and save in **devDependecies**: `npm install <package-name> --save-dev`
- Install and save in **dependencies**: `npm install <package-name> --save`

# ExpressJs-Typescript

## Project setup

Installing following packages as dev-dependencies to work with typescript.

- `npm install --save-dev typescript ts-node @types/node @types/express`

`typescript` is the core package for typescript, `ts-node` is the typescript version of node for runnig `.ts` files just as we do with `node index.js`, In this case we do, `ts-node index.ts`. `@types/node` and `@types/express` has all the types for node and express respectively.

Install core package dependencies as follow.

- `npm install express body-parser cors ......`

## Understanding `package.json`

```js
{
  "name": "demo",
  "version": "1.0.0",
  "description": "demo project",
  "main": "./dist/src/index.js", //primary entry point of your program.
  "scripts": {
    "build": "tsc", // compile ts --> js
    "prepublish": "npm run build",
    "tsc": "tsc -p tsconfig.json", // compile ts --> js with specific configuration specified in tsconfig.json.
    "start": "npm run serve", // run project in prod environment
    "serve": "node dist/src/index.js", // uses compiled js program to run the node project
    "start:dev": "nodemon src/index.ts" // Uses typescript directly to run the program in dev environment.
  },
  "keywords": [],
  "author": "Mohammad Abu Musa Rabiul",
  "license": "ISC",
  "devDependencies": {
    "@types/express": "^4.17.13",
    "@types/node": "^8.0.29",
    "ts-node": "^10.2.0",
    "typescript": "^4.3.5",
    "nodemon": "^2.0.7"
  },
  "dependencies": {
    "dotenv": "^8.2.0",
    "express": "^4.17.1",
    "pg": "^8.4.0",
    "reflect-metadata": "^0.1.10",
    "typeorm": "0.2.31",
    "typeorm-naming-strategies": "^2.0.0"
  }
}
```

## Understanding `tsconfig.json`

**Sample example**
```js
{
  "compilerOptions": {
    "lib": ["es5", "es6"], //Specify a set of bundled library declaration files that describe the target runtime environment.
    "target": "es6", //Set the JavaScript language version for emitted JavaScript and include compatible library declarations.
    "module": "commonjs", //Specify what module code is generated.
    "moduleResolution": "node", //Specify how TypeScript looks up a file from a given module specifier.
    "outDir": "dist", //Specify an output folder for all emitted files
    "emitDecoratorMetadata": true, //Emit design-type metadata for decorated declarations in source files.
    "experimentalDecorators": true, //Enable experimental support for TC39 stage 2 draft decorators.
    "sourceMap": true, //Create source map files for emitted JavaScript files.
    "declaration": false, //Generate .d.ts files from TypeScript and JavaScript files in your project
    "types": ["node"], //Specify type package names to be included without being referenced in a source file.
    "esModuleInterop": true, //Emit additional JavaScript to ease support for importing CommonJS modules. This enables allowSyntheticDefaultImports for type compatibility
    "resolveJsonModule": true, //Enable importing .json files
    "noImplicitAny": false, //Enable error reporting for expressions and declarations with an implied any type..
    "noUnusedLocals": false //Enable error reporting when a local variables aren't read.
  }
}
```
**Useful links**
- https://www.typescriptlang.org/docs/handbook/tsconfig-json.html
- https://www.typescriptlang.org/tsconfig

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

```json
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
