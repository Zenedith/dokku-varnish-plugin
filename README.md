Varnish plugin for Dokku
---------------------------

Project: https://github.com/progrium/dokku

**Warning: This plugin is under development and still only tested with the below dependencies**

Requirements
------------
* Docker version `0.9.0` or higher
* Dokku version `0.2.3` or higher

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
    varnish:create <app>                            Create a varnish container
    varnish:delete <app>                            Delete specified varnish container
    varnish:info <app>                              Display varnish instance informations
    varnish:list                                    Display list of varnish containers
    varnish:logs <app>                              Display last logs from varnish container
```

Simple usage
------------

Set custom configuration for varnish

```bash
$ dokku config:set project VARNISH_GRACE_TTL=30s
$ dokku config:set project VARNISH_GRACE_MAX=1h
$ dokku config:set project VARNISH_CACHE_SIZE=100MB
$ dokku config:set project VARNISH_THROTTLE_LIMIT=255req/30s
```

Create a new varnish instance:

```bash
$ dokku varnish:create project
```

```
-----> Check app name: project
-----> Check varnish dir

-----> Create varnish instance for project
-----> Check app name: project
-----> Check varnish dir

-----> Varnish info for project
-----> Check varnish project

       Host: 172.17.42.1
       Port: 49174

       Backend IP: 172.17.42.1
       Backend Port: 49159

       Cache size: 100MB
       Throttle limit: 255req/30s
       Grace ttl: 30s
       Grace max: 1h
```

Deploy your app with the same name

```bash
$ git remote add dokku git@server:foo
$ git push dokku master
```


Advanced usage
--------------

Deleting varnish instance:

```bash
$ dokku varnish:delete project
```

```
-----> Check app name: project
-----> Check varnish dir

-----> Delete varnish for project
-----> Restore nginx server port to 49159
```

Varnish logs (per database):

```bash
$ dokku varnish:logs project
```

```
-----> Check app name: project
-----> Check varnish dir

-----> Varnish logs for project
child (23) Started
Child (23) said Child starts
Child (23) said SMF.s0 mmap'ed 26214400 bytes of 26214400
```

Varnish informations:

```bash
$ dokku varnish:info project
```

```
-----> Check app name: project
-----> Check varnish dir

-----> Varnish info for project
-----> Check varnish project

       Host: 172.17.42.1
       Port: 49173

       Backend IP: 172.17.42.1
       Backend Port: 49159

       Cache size: 100MB
       Throttle limit: 255req/30s
       Grace ttl: 30s
       Grace max: 1h
```

List of varnish containers:

```bash
$ dokku varnish:list
```

```
-----> Check app name:

-----> List varnish instances
-----> Check varnish dir
-----> Varnish containers:
  - project
```



MIT License
-------

Copyright (c) 2014 Mateusz Stępniak


Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
