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