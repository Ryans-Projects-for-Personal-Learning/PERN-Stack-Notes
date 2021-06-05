---
date: 2021-05-23
title: Environment Variables
categories:
  - general
description: What environment variables are and how to use them.
type: Document
order_number: 1
---
## About

An environment variable is a variable whose value is set outside the program, typically through functionality built into the operating system or microservice. An environment variable is made up of a name/value pair, and any number may be created and available for reference at a point in time.

This is an ideal alternative to hardcoding values as they are convenient and mitigate possible security issues.

## Installation

`npm install dotenv`

## How to Use

In the `server.js` file, type in `require("dotenv").config();` and then create a file called `.env`.

Then create variables with names in all capitals and assign them a value. 

To use an environment variable, type `process.env.[variable name]` where [variable name] is the name of the environment variable.

## Example

Below is an example of creating an environment variable for a port number. In the .env file, there is a variabled called `PORT` which has been assigned a numerical value. It is then referenced in the `server.js` file as seen below. 


```
require ("dotenv").config();
const express = require("express");

const app = express();

const port = process.env.PORT || 3001;
app.listen(port, () => {
    console.log(`server is up and listening on port ${port}`);
});
```
