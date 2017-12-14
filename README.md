# passport-local-postgres

var postgresLocal = require('passport-local-postgres')(pool);
passport.use(new LocalStrategy(postgresLocal.localStrategy));
passport.serializeUser(postgresLocal.serializeUser);
passport.deserializeUser(postgresLocal.deserializeUser);