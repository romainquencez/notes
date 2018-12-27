# Django

## Table of contents

* [Access from remote to local server](#access-from-remote-to-local-server)
* [Fixtures](#fixtures)
  * [Dump data from database](#dump-data-from-database)
  * [Load data to database](#load-data-to-database)
* [Migrations](#migrations)

## Access from remote to local server

* Open `webpack-<app>-dev.config.js` and `webpack-admin-dev.config.js`.
* Replace `localhost` by server's IP address.
* Restart server.

## Fixtures

Useful for dump or load from/to database.

### Dump data from database

https://docs.djangoproject.com/en/1.11/ref/django-admin/#dumpdata

```bash
dumpdata <model>
```

* `<model>` model name to dump data from. One or many.
* `[--output <file>]` Dump data to specified file. If not specified, dump data to console.
* `[--format <format>]` Data format. YAML by default, or XML.
* `[--natural-foreign]` Use natural keys for foreign relations.
* `[--natural-primary]` Same, but for primary keys.
* `[--pks <pk>]` Dump only specified pks. Useful for dumping only one entry for example.

### Load data to database

https://docs.djangoproject.com/en/1.11/ref/django-admin/#loaddata

```bash
loaddata <file>
```

* `<file>` File with data to load. Can be in fixtures folder, in FIXTURE_DIRS, or at project's root.

## Migrations

* `showmigrations` List all migrations.
* `makemigrations` Make new migrations if a model has changed.
* `migrate` Execute new migrations.
