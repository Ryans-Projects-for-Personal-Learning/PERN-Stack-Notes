---
date: 2021-05-23
title: Express Setup
categories:
  - express
description: Getting Started with Express
type: Document
order_number: 1
---
## About

Express.js is a back end web application framework for node.js. 

## Installation

`npm install express`

## How to Use
In the `server.js` file, type in

```
require ("dotenv").config();
const express = require("express");

const app = express();

const port = process.env.PORT || 3001;
app.listen(port, () => {
    console.log(`server is up and listening on port ${port}`);
});
```

## Connecting Express to Postgres

1. Assign environment variables for database connection details.

```
PGHOST='localhost'
PGUSER=process.env.USER
PGDATABASE=process.env.USER
PGPASSWORD=null
PGPORT=5432
```

2. Create a folder called db and create a folder called index.js

3. In index.js, paste the following.

```
const { text } = require("express");
const { Pool} = require("pg");

const pool = new Pool();

module.exports = {
    query: (text,params) => pool.query(text,params),
};
```

* `{ Pool } = require("pg");` imports the `pg` library.
* `const pool = new Pool()` Connects the app to the database.
* `module.exports = {query: (text,params) => pool.query(text,params)}` allows us to execute query statements. 
