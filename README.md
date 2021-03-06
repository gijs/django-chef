django-chef
===========

This is meant to be a blank [django][1] project template that uses [Chef][2] to
provision the server where your application will be deployed. It also uses
[Vagrant][3] to create the same environment in a Virtualbox VM.

I have made some choices as to how the django application will be deployed.
This is based on the content and recommendations stemming from [Djangocon
2011][4]. The following will be installed.

* Ubuntu server
* nginx
* gunicorn
* postgresql
* memcached
* rabbitmq
* celery

Of course, other small applications will be installed to ensure smoother
execution:

* virtualenv & pip
* git
* Python driver for postgresql
* etc


Usage
-----

* Install [Vagrant][3]
* Download the `lucid64` box and add it as `base`
* Your django project should live in `coolname`. (i.e. `coolname/settings.py`)
* Please change the name of the directory to match your project
* The name of the project has to be changed in a few other places
    * `fabfile.py`
    * `node.json`
* Run `vagrant up` to build the VM
* Then run `fab -R vagrant bootstrap` which will create a virtualenv, load your
  code, install dependencies, sync your db, etc.


Vagrant roledef for fabric
--------------------------

The main `fabfile` includes some special logic to work around some of the
limitations of vagrant. Nothing too hacky though. Every time you want to
execute something on your local VM, include the `-R vagrant` flag.

Vagrant code reloading
----------------------

If you run your code in a Vagrant VM, a file watcher is automatically started.
This watcher will detect changes in your source code and reload gunicorn. This
emulates the behavior of Django's built-in web server.


[1]: https://www.djangoproject.com/
[2]: http://www.opscode.com/chef/
[3]: http://vagrantup.com/
[4]: http://djangocon.us/
