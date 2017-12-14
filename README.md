# passport-local-postgres

Passport-Local Postgres is a [Postgres](https://www.postgresql.org/) plugin 
that simplifies building username and password login with [Passport](http://passportjs.org).

## Installation

```bash
#npm
$ npm install passport-local-postgres --save

#yarn
$ yarn add passport-local-postgres
```

Passport-Local Mongoose does not require `passport`, `passport-local` or `postgress` dependencies directly but expects you
to have these dependencies installed.

In case you need to install the whole set of dependencies

```bash
#npm
$ npm install passport passport-local pg passport-local-postgres --save

#yarn
$ yarn add passport passport-local pg passport-local-postgres
```

## Usage

### Plugin Passport-Local Passport
First you need to plugin Passport-Local Post into your User schema

```javascript
const passport = require('passport');
const LocalStrategy = require('passport-local').Strategy;
const pg = require('pg');
const parseDbUrl = require('parse-database-url');

const pool = new pg.Pool(parseDbUrl(process.env.DATABASE_URL))
pool.on('error', function (err) {
  console.log('idle client error', err.message, err.stack);
})

var postgresLocal = require('passport-local-postgres')(pool);
```

#### Simplified Passport/Passport-Local Configuration

```javascript
passport.use(new LocalStrategy(postgresLocal.localStrategy));
passport.serializeUser(postgresLocal.serializeUser);
passport.deserializeUser(postgresLocal.deserializeUser);
```

