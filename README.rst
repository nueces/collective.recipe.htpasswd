========================================
Buldout recipe for create htpasswd files
========================================

.. contents::


Introdution
===========

This recipe can be used to generate files for basic authentication of HTTP
users, to restrict the access to HTTP resoruces. The aim is to be fully
compatible with the `htpasswd program`_ that come with the
`Apache httpd Server`_, and support all the `password formats`_ that it
supports. This formats, with some minor diffenrences in the case of the plain
method, are also `supported by the auth_basic module`_ of the nginx http server.

At this moment this recipe support plain and crypt algorithms for storage
passwords. The crypt algorithm is based on the system's crypt() routine, so it
inherits its limitations (see: `man 5 crypt`_).


*Note:* The plaintext passowrds are only accepted by the Apache httpd server on
Windows and Netware.

*Caution:* This recipe should not be used to update an existing htpasswd file,
because it overwritte the htpasswd file in every update.

Example usage
=============

The simplest way to use this recipe is to add a part in ``buildout.cfg`` like
this:

.. code-block:: ini

    [buildout]
    parts = htpasswd

    [htpasswd]
    recipe = collective.recipe.htpasswd
    output = ${buildout:directory}/etc/htpasswd
    credentials =
        nueces:secret
        nutz:crackme


Supported options
=================

* output: Specify a path to the output file. The path will be created if it does
  not exist.
* credentials: One set per line of credentials formed by username and password separated by a
  colon. e.g. <username>:<password>.
* mode: Specified with octal numbers, as in the chmod program. e.g. 640. If it
  not set the file are created with the mask mode from the system enviroment.
* algorithm: The supported options are 'crypt' and 'plain'. Default to 'cypt'.


Development
===========

- Code repository: http://github.com/nueces/collective.recipe.htpasswd
- Report bugs at http://github.com/nueces/collective.recipe.htpasswd/issues


.. _htpasswd program: http://httpd.apache.org/docs/2.4/programs/htpasswd.html
.. _Apache httpd server: http://httpd.apache.org/
.. _password formats: http://httpd.apache.org/docs/2.2/misc/password_encryptions.html
.. _supported by the auth_basic module: http://nginx.org/en/docs/http/ngx_http_auth_basic_module.html#auth_basic
.. _man 5 crypt: http://manpages.debian.net/cgi-bin/man.cgi?query=crypt&sektion=3
