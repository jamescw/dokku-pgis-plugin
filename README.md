PostGIS plugin for Dokku
------------------------

Project: https://github.com/progrium/dokku

**Warning: This plugin is under development and still only tested with the below dependencies**

Requirements
------------
* Docker version `0.7.2` or higher
* Dokku version `0.2.1` or higher

Installation
------------
```
cd /var/lib/dokku/plugins
git clone https://github.com/fermuch/dokku-pg-plugin.git postgis
dokku plugins-install
```


Commands
--------
```
$ dokku help
    postgresql:create <db>                         Create a PostgreSQL container
    postgresql:delete <db>                         Delete specified PostgreSQL container
    postgresql:dump <db> > dump_file.sql           Dump database data
    postgresql:info <db>                           Display database informations
    postgresql:link <app> <db>                      Link an app to a PostgreSQL database
    postgresql:list                                 Display list of PostgreSQL containers
    postgresql:logs <db>                           Display last logs from PostgreSQL container
    postgresql:restore <db> < dump_file.sql        Restore database data from a previous dump
```

Simple usage
------------

Create a new DB:
```
$ dokku postgis:create foo            # Server side
$ ssh dokku@server postgis:create foo # Client side

-----> PostGIS container created: postgis/foo

       Host: 172.17.42.1
       User: 'root'
       Password: 'RDSBYlUrOYMtndKb'
       Database: 'db'
       Public port: 49187
```

Deploy your app with the same name (client side):
```
$ git remote add dokku git@server:foo
$ git push dokku master

```

Link your app to the database
```bash
dokku postgis:link app_name database_name
```


Advanced usage
--------------

Inititalize the database with SQL statements:
```
cat init.sql | dokku postgis:create foo
```

Deleting databases:
```
dokku postgis:delete foo
```

Linking an app to a specific database:
```
dokku postgis:link foo bar
```

postgis logs (per database):
```
dokku postgis:logs foo
```

Database informations:
```
dokku postgis:info foo
```

List of containers:
```
dokku postgis:list
```

Dump a database:
```
dokku postgis:dump foo > foo.sql
```

Restore a database:
```
dokku postgis:restore foo < foo.sql
```
