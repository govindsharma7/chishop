Installation using virtualenv
::

    $ git clone git://github.com/saltycrane/chishop.git saltycrane-chishop
    $ cd saltycrane-chishop/
    $ virtualenv venv
    $ source venv/bin/activate
    $ pip install -r requirements.txt
    $ pip install -e ./
    $ cp chishop/settings.py.sample chishop/settings.py
    $ cd chishop
    $ ./manage.py syncdb
    $ ./manage.py migrate
    $ ./manage.py runserver

=========================================
ChiShop/DjangoPyPI
=========================================
:Version: 0.1

Installation
============

Install dependencies::

    $ python bootstrap.py
    $ ./bin/buildout

Initial configuration
---------------------
::

    $ cp chishop/settings.py.sample chishop/settings.py
    $ $EDITOR chishop/settings.py
    $ ./bin/django syncdb && ./bin/django migrate

Run the PyPI server
-------------------
::

    $ ./bin/django runserver

Please note that ``chishop/media/dists`` has to be writable by the
user the web-server is running as.

In production
-------------

You may want to copy the file ``chishop/production_example.py`` and modify
for use as your production settings; you will also need to modify
``bin/django.wsgi`` to refer to your production settings.

Using Setuptools
================

Add the following to your ``~/.pypirc`` file::

    [distutils]
    index-servers =
        pypi
        local


    [pypi]
    username:user
    password:secret

    [local]

    username:user
    password:secret
    repository:http://localhost:8000

Uploading a package: Python >=2.6
--------------------------------------------

To push the package to the local pypi::

    $ python setup.py register -r local sdist upload -r local


Uploading a package: Python <2.6
-------------------------------------------

If you don't have Python 2.6 please run the command below to install the backport of the extension::

     $ easy_install -U collective.dist

instead of using register and dist command, you can use "mregister" and "mupload", that are a backport of python 2.6 register and upload commands, that supports multiple servers.

To push the package to the local pypi::

    $ python setup.py mregister -r local sdist mupload -r local

.. # vim: syntax=rst expandtab tabstop=4 shiftwidth=4 shiftround
