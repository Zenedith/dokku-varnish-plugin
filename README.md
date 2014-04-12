Varnish plugin for Dokku
---------------------------

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
git clone https://github.com/Zenedith/dokku-varnish-plugin varnish
dokku plugins-install
```


Commands
--------
```
$ dokku help
    varnish:create <app>                            Create a Varnish container
    varnish:delete <app>                            Delete specified Varnish container
    varnish:info <app>                              Display varnish instance informations
    varnish:list                                    Display list of Varnish containers
    varnish:logs <app>                              Display last logs from Varnish container
```

Simple usage
------------

Create a new DB:
```
$ dokku varnish:create foo            # Server side
$ ssh dokku@server varnish:create foo # Client side

-----> Varnish container created: varnish/foo

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
dokku varnish:link app_name database_name
```


Advanced usage
--------------

Inititalize the database with SQL statements:
```
cat init.sql | dokku varnish:create foo
```

Deleting databases:
```
dokku varnish:delete foo
```

Linking an app to a specific database:
```
dokku varnish:link foo bar
```

Varnish logs (per database):
```
dokku varnish:logs foo
```

Database informations:
```
dokku varnish:info foo
```

List of containers:
```
dokku varnish:list
```

Dump a database:
```
dokku varnish:dump foo > foo.sql
```

Restore a database:
```
dokku varnish:restore foo < foo.sql
```

MIT License
-------

Copyright (c) 2014 Mateusz Stępniak


Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.